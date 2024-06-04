mvn install -DskipTests -Dmaven.test.skip

git config --global credential.helper cache

yarn install --registry=https://registry.npmjs.org/

yarn install --registry=https://registry.npmmirror.com/

npm publish --registry=https://registry.npmjs.org/ --access public

git config --global http.proxy http://127.0.0.1:7890

defaults write com.apple.finder AppleShowAllFiles -boolean true ; killall Finder

git config --global branch.autosetuprebase always
git config --global pull.rebase false

git pull --no-rebase

'(.[\u4E00-\u9FA5]+)|([\u4E00-\u9FA5]+.)'
