> 本文详细地阐述了 Redux 的设计理念与实践技巧，包含了其三大原则与简单的仿制、基础组件以及 React 集成使用、基于 Thunk, Promise, Sagas 三种不同的异步处理方式、Selector, Ducks 等其他常见的样式规范、中间件的实现原理与代码分析等。

# Redux CheatSheet | Redux 设计理念与实践技巧清单

Redux 是受 Flux 启发的，类似于 Event Sourcing 的事件驱动型框架。

# 基础组件

# 实践工具

# ducks

[ducks-modular-redux](https://github.com/erikras/ducks-modular-redux) 是对于 Ducks 规范的描述，其按照业务模块将 reducer, action, actionTypes 合并到单一的文件中。

```js
// widgets.js

// Actions
const LOAD = "my-app/widgets/LOAD";
const CREATE = "my-app/widgets/CREATE";
const UPDATE = "my-app/widgets/UPDATE";
const REMOVE = "my-app/widgets/REMOVE";

// Reducer
export default function reducer(state = {}, action = {}) {
  switch (action.type) {
    // do reducer stuff
    default:
      return state;
  }
}

// Action Creators
export function loadWidgets() {
  return { type: LOAD };
}

export function createWidget(widget) {
  return { type: CREATE, widget };
}

export function updateWidget(widget) {
  return { type: UPDATE, widget };
}

export function removeWidget(widget) {
  return { type: REMOVE, widget };
}

// side effects, only as applicable
// e.g. thunks, epics, etc
export function getWidget() {
  return dispatch =>
    get("/widget").then(widget => dispatch(updateWidget(widget)));
}
```

A module...

MUST export default a function called reducer()
MUST export its action creators as functions
MUST have action types in the form npm-module-or-app/reducer/ACTION_TYPE
MAY export its action types as UPPER_SNAKE_CASE, if an external reducer needs to listen for them, or if it is a published reusable library

在外部使用时，我们可以导出默认的 reducer:

```js
import { combineReducers } from "redux";
import * as reducers from "./ducks/index";

const rootReducer = combineReducers(reducers);
export default rootReducer;
```

在组件中，可以导出所有的 Action:

```js
import * as widgetActions from "./ducks/widgets";
```

# redux-actions

```js
import { createActions, handleActions, combineActions } from "redux-actions";

const defaultState = { counter: 10 };

const { increment, decrement } = createActions({
  INCREMENT: (amount = 1) => ({ amount }),
  DECREMENT: (amount = 1) => ({ amount: -amount })
});

const reducer = handleActions(
  {
    INCREMENT: (state, action) => ({
      counter: state.counter + action.payload
    }),

    DECREMENT: (state, action) => ({
      counter: state.counter - action.payload
    })
  },
  defaultState
);

const reducer = handleActions(
  {
    [combineActions(increment, decrement)](
      state,
      {
        payload: { amount }
      }
    ) {
      return { ...state, counter: state.counter + amount };
    }
  },
  defaultState
);

export default reducer;
```

```js
import { createStore, applyMiddleware } from 'redux';
import promiseMiddleware from 'redux-promise-middleware';
import thunkMiddleware from 'redux-thunk';
import logger from 'redux-logger';

const reducer = (state = {}, action) => {
  ...
}

const store = createStore(reducer, {}, applyMiddleware(
  thunkMiddleware,
  promiseMiddleware(),
  logger,
));

export default store;
```

```js
const promiseAction = () => ({
  type: "PROMISE",
  payload: Promise.resolve()
});
```

# Async Actions | 异步 Action 处理

## Thunk

## Promise

[redux-promise](https://github.com/redux-utilities/redux-promise) 会自动处理 payload 为 Promise 对象的 Action，并且会分发该 Action 的副本，包含了 Promise 的处理结果，并且根据处理结果动态设置了 status 属性为 `success` 或者 `error`。

```js
// 创建简单的异步 Action
createAction("FETCH_THING", async id => {
  const result = await somePromise;
  return result.someValue;
});

// 与自定义的 WebAPI 协同使用
import { WebAPI } from "../utils/WebAPI";

export const getThing = createAction("GET_THING", WebAPI.getThing);
export const createThing = createAction("POST_THING", WebAPI.createThing);
export const updateThing = createAction("UPDATE_THING", WebAPI.updateThing);
export const deleteThing = createAction("DELETE_THING", WebAPI.deleteThing);
```

[redux-promise-middleware](https://github.com/pburtchaell/redux-promise-middleware) 为我们提供了类似的异步处理功能，其能够接受某个 Promise，并且依次分发 Pending, Fulfilled, 以及 Rejected 这几个不同状态的 Action:

```js
const promiseAction = () => ({
  type: "PROMISE",
  payload: Promise.resolve()
});
```

该工具同样可以与 Redux Thunk 协同使用，来进行多个 Action 的分发：

```js
const secondAction = data => ({
  type: "TWO",
  payload: data
});

const first = () => {
  return dispatch => {
    const response = dispatch({
      type: "ONE",
      payload: Promise.resolve()
    });

    response.then(data => {
      dispatch(secondAction(data));
    });
  };
};
```

我们也可以自己实现 Promise 中间件，可以参考 [redux/promiseMiddleware](https://github.com/wx-chevalier/coding-snippets/tree/master/web/redux) 的源代码实现。在实际应用中，我们往往需要等待某个操作处理结束进行刷新等附加响应；此时我们即可以创建自定义的 Thunk，也可以直接在类方法中使用 await 来等待 dispatch 函数返回的 Promise:

```js
const { fetchThing } = bindActionCreators({ fetchThing }, dispatch);

// 这里即会在 Redux 中分发 Action，同样也会阻塞执行直至 Promise 处理完毕
await fetchThing().payload;
```

## Sagas

Sagas 是源于[计算机科学与技术](http://www.cs.cornell.edu/andru/cs711/2002fa/reading/sagas.pdf)的概念，用于描述事务及其关联处理操作的约束。[redux-sagas](https://github.com/redux-saga/) 的官方描述是用于处理副作用(Side Effects)的 Redux 中间件，允许我们以同步地方式编写异步代码，并使用 try-catch 进行异常处理。

![redux-saga-dataflow](https://user-images.githubusercontent.com/5803001/40041848-05f758a2-5852-11e8-9ff5-12a9ff8046aa.png)

与 redux-thunk 相比，[redux-sagas](https://github.com/redux-saga/) 并不是直接从 UI 调用逻辑代码，而是进行纯粹地 dispatch action；所有的异步流程控制都被移入到了 sagas，从而增强组件与逻辑代码的可复用性与可测试性。redux-sagas 基于 ES6 Generator，能为我们提供高级的异步控制流以及并发管理，可以使用简单的同步方式描述异步流，并通过 fork 实现并发任务。

![8cc1a873-c675-9009-570d-9684da4a704f](https://user-images.githubusercontent.com/5803001/40041849-063158b8-5852-11e8-9e24-39bcbdef83a4.png)

参考 [fe-boilerplate/redux](https://parg.co/YA2) 的示例，我们首先需要引入并且创建 Sagas 中间件实例：

```js
import createSagaMiddleware from 'redux-saga';
import rootSaga from '../sagas/sagas';

const sagaMiddleware = createSagaMiddleware();

// 引入中间件，并构建 Store 对象
...

sagaMiddleware.run(rootSaga);
```

这里的 sagas 文件，即包含了具体的逻辑处理代码：

```js
// helloSaga 会在 sagaMiddleware.run 时即刻执行
export function* helloSaga() {
  console.log("Hello Saga!");
}

// worker saga
export function* incrementAsync() {
  yield call(delay, 1000);
  // 继续分发事件
  yield put({ type: "SAGA_INCREMENT" });
}

// watcher saga
export function* watchIncrementAsync() {
  // 监听 Action，并执行关联操作
  yield takeEvery("SAGA_INCREMENT_ASYNC", incrementAsync);
}

// root saga
export default function* rootSaga() {
  yield [helloSaga(), watchIncrementAsync()];
}
```

Sagas 为我们定义了三种不同的 Saga，其中 Worker Saga 负责 API 调用、异步请求、结果处理等具体的任务；Watcher Saga 则监听被 dispatch 的 actions，当接收到 action 或者知道其被触发时，调用 worker saga 执行任务。而 Root Saga 则是立即启动 Sagas 的唯一入口。Saga 使用 Generator 函数来 yield Effect，其利用生成器可以暂停执行，再次执行的时候从上次暂停的地方继续执行的特性。Effect 是一个简单的对象，该对象包含了一些给 middleware 解释执行的信息。可以通过使用 effects API，如 fork，call，take，put，cancel 等来创建 Effect。

如 `yield call(fetch, '/user')` 即 `yield` 了下面的对象，`call` 创建了一条描述结果的信息，然后，`redux-saga` middleware 将确保执行这些指令并将指令的结果返回给生成器：

```
{
  type: CALL,
  function: fetch,
  args: ['/user']
}
```

我们也可以并发执行多个任务：

```js
const [users, repos] = yield[(call(fetch, "/users"), call(fetch, "/repos"))];
```

同样以常见的接口请求，与结果处理为例：

```js
import { take, fork, call, put } from "redux-saga/effects";

// The worker: perform the requested task
function* fetchUrl(url) {
  // 指示中间件调用 fetch 异步任务
  const data = yield call(fetch, url);

  // 指示中间件发起一个 action 到 Store
  yield put({ type: "FETCH_SUCCESS", data });
}

// The watcher: watch actions and coordinate worker tasks
function* watchFetchRequests() {
  while (true) {
    // 指示中间件等待 Store 上指定的 action，即监听 action
    const action = yield take("FETCH_REQUEST");

    // 指示中间件以无阻塞调用方式执行 fetchUrl
    yield fork(fetchUrl, action.url);
  }
}
```

# 样式风格

## ducks

## redux-actions

```js
import { createActions, handleActions, combineActions } from "redux-actions";

const defaultState = { counter: 10 };

const { increment, decrement } = createActions({
  INCREMENT: (amount = 1) => ({ amount }),
  DECREMENT: (amount = 1) => ({ amount: -amount })
});

const reducer = handleActions(
  {
    INCREMENT: (state, action) => ({
      counter: state.counter + action.payload
    }),

    DECREMENT: (state, action) => ({
      counter: state.counter - action.payload
    })
  },
  defaultState
);

const reducer = handleActions(
  {
    [combineActions(increment, decrement)](
      state,
      {
        payload: { amount }
      }
    ) {
      return { ...state, counter: state.counter + amount };
    }
  },
  defaultState
);

export default reducer;
```

```js
import { createStore, applyMiddleware } from 'redux';
import promiseMiddleware from 'redux-promise-middleware';
import thunkMiddleware from 'redux-thunk';
import logger from 'redux-logger';

const reducer = (state = {}, action) => {
  ...
}

const store = createStore(reducer, {}, applyMiddleware(
  thunkMiddleware,
  promiseMiddleware(),
  logger,
));

export default store;
```

```js
const promiseAction = () => ({
  type: "PROMISE",
  payload: Promise.resolve()
});
```

# Middleware | 中间件

# 实践的思考

[现代 Web 开发/状态管理](https://parg.co/G8D)

Redux 适合于需要强项目健壮度与多人协调规范的大中型团队，对于很多中小型创业性质，项目需求迭代异常快的团队则往往可能起到适得其反的作用。如果你真的喜欢 Redux，那么更应该在合适的项目，合适的阶段去接入 Redux，而不是在需求尚未成型之处就花费大量精力搭建复杂的脚手架，说不准客户的需求图纸都画反了呢。Dan 推荐的适用 Redux 的情况典型的有：

- [方便地能够将应用状态存储到本地并且重启动时能够读取恢复状态](https://egghead.io/lessons/javascript-redux-persisting-the-state-to-the-local-storage?course=building-react-applications-with-idiomatic-redux)

- [方便地能够在服务端完成初始状态设置，并且完成状态的服务端渲染](http://redux.js.org/docs/recipes/ServerRendering.html)

- [能够序列化记录用户操作，能够设置状态快照，从而方便进行 Bug 报告与开发者的错误重现](https://github.com/dtschust/redux-bug-reporter)

- [能够将用户的操作或者事件传递给其他环境而不需要修改现有代码](https://github.com/philholden/redux-swarmlog)

- [能够添加重放或者撤销功能而不需要重构代码](http://redux.js.org/docs/recipes/ImplementingUndoHistory.html)

- [能够在开发过程中实现状态历史的回溯，或者根据 Action 的历史重现状态](https://github.com/gaearon/redux-devtools)

- [能够为开发者提供全面透彻的审视和修改现有开发工具的接口，从而保证产品的开发者能够根据他们自己的应用需求打造专门的工具](https://github.com/romseguy/redux-devtools-chart-monitor)

- [能够在复用现在大部分业务逻辑的基础上构造不同的界面](https://youtu.be/gvVpSezT5_M?t=11m51s)

仅就笔者的个人实践而言，在

对于数据的获取

对于简单可重复的全局状态，譬如通用的接口返回的错误信息，可以使用全局的错误状态：

```js
function reducer(state, { payload }) {
  if (payload.error) {
    return {
      ...state,
      errorMessage: payload.error.message
    };
  }
}
```

如果是复杂接口响应的处理，譬如创建或者更新的表单，特别是还需要包含大量的非跨组件的 UI 操作，那么不妨使用本地状态处理，当然也可以使用 Thunk 函数进行处理：

```js
class Com extends Component {
  async handleSubmit() {
    try {
      const result = await doMutation();

      if (result.success) {
        // 执行成功之后的界面操作
        showSuccessMessage();
        fetchThing();
        closeModal();
      } else {
        // 执行失败之后的部分操作
        doFallback();
      }
    } catch (e) {
      showErrorMessage();
    }
  }
}
```

# 关键源代码

## react-redux

在 Provider.js 中：

```

```
