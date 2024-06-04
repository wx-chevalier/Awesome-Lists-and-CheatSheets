# 符号

# 希腊字母

# 运算符号

## 逻辑运算符

- $\because$（`\because`）

  ∴：\therefore
  ∀：\forall
  ∃：\exists
  ≠：\not=
  ≯：\not>
  ⊄：\not\subset

# 运算

^表示上标，
\_表示下标，
如果上（下）标内容多于一个字符就需要使用{}，注意不是( ), 因为( )经常是公式本身组成部分，为避免冲突，所以选用了{ } 将其包起来。

示例：$x^{y^z}=(1+e^x)^{-2xy^w}$

效果：xyz=(1+ex)−2xyw
上面输入的上下标都是在字符的右侧，要想在左侧或者两侧都写上下标，那么需要使用\sideset 语法。

示例：$\sideset{^1_2}{^3_4}\bigotimes$

效果：12⨂34

3.3 括号和分隔符

( )和[ ]就是自身了，由于{ } 是 Tex 的元字符，所以表示它自身时需要转义。

示例：$f(x,y) = x^2 + y^2, x\epsilon[0,100]$

效果：f(x,y)=x2+y2,xϵ[0,100]
有时候括号需要大号的，普通括号不好看，此时需要使用\left 和\right 加大括号的大小。

示例：$(\frac{x}{y})^8，\left(\frac{x}{y}\right)^8$

效果：(xy)8，(xy)8
\left 和\right 必须成对出现，对于不显示的一边可以使用 . 代替。

示例：$\left.\frac{{\rm d}u}{{\rm d}x} \right| _{x=0}$

效果：dudx∣∣x=0
3.4 分数

使用\frac{分子}{分母}格式，或者 分子\over 分母。

示例：$\frac{1}{2x+1}或者1\over{2x+1}$

效果：12x+1 或者 12x+1
3.5 开方

示例：$\sqrt[9]{3}和\sqrt{3}$

效果：3‾‾√9 和 3‾‾√
3.6 省略号

有两种省略号，\ldots 表示语文本底线对其的省略号，\cdots 表示与文本中线对其的省略号。

示例：$f(x_1, x_2, \ldots, x_n)=x_1^2 + x_2^2+ \cdots + x_n^2$

效果：f(x1,x2,…,xn)=x21+x22+⋯+x2n
3.7 矢量

示例：$\vec{a} \cdot \vec{b}=0$

效果: a⃗ ⋅b⃗ =0
3.8 积分

示例：$\int_0^1x^2{\rm d}x $

效果：∫10x2dx
3.9 极限

示例：$\lim_{n\rightarrow+\infty}\frac{1}{n(n+1)}$

效果：limn→+∞1n(n+1)
3.10 累加、累乘

示例：$\sum_1^n\frac{1}{x^2}，\prod_{i=0}^n\frac{1}{x^2}$

效果：∑n11x2，∏ni=01x2
3.11 希腊字母

希腊字符示例：$$\alpha　A　\beta　B　\gamma　\Gamma　\delta　\Delta　\epsilon　E \varepsilon　　\zeta　Z　\eta　H　\theta　\Theta　\vartheta \iota　I　\kappa　K　\lambda　\Lambda　\mu　M　\nu　N \xi　\Xi　o　O　\pi　\Pi　\varpi　　\rho　P \varrho　　\sigma　\Sigma　\varsigma　　\tau　T　\upsilon　\Upsilon \phi　\Phi　\varphi　　\chi　X　\psi　\Psi　\omega　\Omega$$

效果：

α 　 A 　 β 　 B 　 γ 　 Γ 　 δ 　 Δ 　 ϵ 　 Eε 　　 ζ 　 Z 　 η 　 H 　 θ 　 Θ 　 ϑι 　 I 　 κ 　 K 　 λ 　 Λ 　 μ 　 M 　 ν 　 Nξ 　 Ξ 　 o 　 O 　 π 　 Π 　 ϖ 　　 ρ 　 Pϱ 　　 σ 　 Σ 　 ς 　　 τ 　 T 　 υ 　 Υϕ 　 Φ 　 φ 　　 χ 　 X 　 ψ 　 Ψ 　 ω 　 Ω

3.12 数学符号大汇总
±：\pm
×：\times
÷：\div
∣：\mid

⋅：\cdot
∘：\circ
∗: \ast
⨀：\bigodot
⨂：\bigotimes
⨁：\bigoplus
≤：\leq
≥：\geq
≠：\neq
≈：\approx
≡：\equiv
∑：\sum
∏：\prod
∐：\coprod

集合运算符：
∅：\emptyset
∈：\in
∉：\notin
⊂：\subset
⊃：\supset
⊆：\subseteq
⊇：\supseteq
⋂：\bigcap
⋃：\bigcup
⋁：\bigvee
⋀：\bigwedge
⨄：\biguplus
⨆：\bigsqcup

对数运算符：
log：\log
lg：\lg
ln：\ln

三角运算符：
⊥：\bot
∠：\angle
30∘：30^\circ
sin：\sin
cos：\cos
tan：\tan
cot：\cot
sec：\sec
csc：\csc

微积分运算符：
y′x：\prime
∫：\int
∬：\iint
∭：\iiint
⨌：\iiiint
∮：\oint
lim：\lim
∞：\infty
∇：\nabla

戴帽符号：
ŷ：\hat{y}
yˇ：\check{y}
y˘：\breve{y}

连线符号：
a+b+c+d⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯：\overline{a+b+c+d}
a+b+c+d⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯：\underline{a+b+c+d}
a+b+c⏟1.0+d2.0：\overbrace{a+\underbrace{b+c}\_{1.0}+d}^{2.0}

箭头符号：
↑：\uparrow
↓：\downarrow
⇑：\Uparrow
⇓：\Downarrow
→：\rightarrow
←：\leftarrow
⇒：\Rightarrow
⇐：\Leftarrow
⟶：\longrightarrow
⟵：\longleftarrow
⟹：\Longrightarrow
⟸：\Longleftarrow

3.13 需要转义的字符

要输出字符　空格　#　$　%　&　\_　{　}　，用命令：　\空格　#　\$　\%　\&　\_　{　}

3.14 使用指定字体

{\rm text}如：
使用罗马字体：text text
其他的字体还有：
\rm 　　罗马体　　　　　　　\it 　　意大利体
\bf 　　黑体　　　　　　　　\cal 　花体
\sl 　　倾斜体　　　　　　　\sf 　　等线体
\mit 　数学斜体　　　　　　\tt 　　打字机字体
\sc 　　小体大写字母

# Links

- https://wenku.baidu.com/view/fd741028453610661ed9f458.html?from=search
