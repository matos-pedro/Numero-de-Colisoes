# $`\pi`$ = count(:black_circle::boom: :red_circle:) ?

Esse texto se inspira no problema apresentado no vídeo ["The most unexpected answer to a counting puzzle"](https://www.youtube.com/watch?v=HEfHFsfGXjs) e apresenta uma solução a sua maneira. 

O problema: 
um bloco de massa $`m`$ é colocado entre uma parede imóvel e um bloco de massa $`M`$ que se desloca em direção ao primeiro bloco. Se $M>m$ e considerarmos que as colisões são elásticas, qual o número total de colisões experimentada pelos três elementos? 

## Primeira Abordagem
### Condições Iniciais
Vamos adotar a seguinte convenção: 


1. o problema é unidimensional;
2. da esquerda para a direita estão a parede, o bloco menor e o bloco maior; 
3. a posição da parede é definida como sendo a origem de nosso sistema, onde $x=0$; a direita da parede, $x>0$.
4. velocidade negativa representa o movimento da direita para a esquerda;
5. as velocidades $u$ e $v$ representam as velocidades dos blocos menor e maior;  
6. o experimento se inicia com o bloco de massa menor imóvel - massa $m$  e velocidade $u_0=0$ - entre a parede e o bloco de massa maior $M$, que possui velocidade $v_0 = -V_0 < 0$.  

Dado o problema, duas colisões são possíveis: do bloco menor com o bloco maior, e do bloco menor com a parede.

### M-m Collision
Partindo das conservações de quantidade de movimento e energia cinética, a primeira colisão entre os dois blocos levará o sistema a um novo estado '1' tal que: 
```math
\begin{align} \tag{1} \frac{mu_1^2}{2} + \frac{Mv_1^2}{2} =\frac{mu_{0}^2}{2} + \frac{Mv_{0}^2}{2}\end{align}
```

```math
mu_1 + Mv_1 = mu_0 + Mv_0
```

A solução desse sistema de equações nos leva às novas velocidades $u_1$ e $v_1$ definidas por:
```math
\begin{align}
u_1 = \frac{m-M}{m+M}u_0 + \frac{2M}{m+M}v_0\\
v_1 = \frac{2m}{m+M}u_0 + \frac{M-m}{m+M}v_0
\end{align}
```

Por conveniência, vamos definir $\alpha = \sqrt{m/M}$ de modo que possamos expressar $u_1$ e $v_1$ em notação matricial como: 

```math
\tag{2}\begin{bmatrix} u_1 \\ v_1  \end{bmatrix} = \left(\frac{1}{1+\alpha^2}\right) \begin{bmatrix} \alpha^2-1 & 2 \\ 2\alpha^2 & 1-\alpha^2  \end{bmatrix} \begin{bmatrix} u_0 \\ v_0  \end{bmatrix},
```
válido para quaisquer $u_0$ e $v_0$.

### m-wall Collision
Podemos observar da equação 2 que após a primeira colisão, $u_1$ terá velocidade negativa (mesmo sentido que $v_0$) e portando, irá eventualmente colidir com a parede. Sendo esta uma colisão elástica, podemos afirmar que o estado '2' resultante dessa segunda colisão é:

```math
\tag{3}\begin{bmatrix} u_2 \\ v_2  \end{bmatrix} = \begin{bmatrix} -u_1 \\ v_1  \end{bmatrix} = \begin{bmatrix} -1 & 0 \\ 0 & 1 \end{bmatrix} \begin{bmatrix} u_1 \\ v_1  \end{bmatrix}.
```

Unindo os resultados das equações 2 e 3, chegamos a 

```math
\begin{bmatrix} u_2 \\ v_2  \end{bmatrix} = \left(\frac{1}{1+\alpha^2}\right)\begin{bmatrix} -1 & 0 \\ 0 & 1 \end{bmatrix} \begin{bmatrix} \alpha^2-1 & 2 \\ 2\alpha^2 & 1-\alpha^2  \end{bmatrix}\begin{bmatrix} u_0 \\ v_0  \end{bmatrix}
```

Para fins de simplificação, vamos assumir que as colisões sempre ocorrem aos pares, com uma colisão m-parede SEMPRE sucedendo uma colisão m-M. Se estivermos errados quanto à última colisão, estaremos errando o número total de colisões em +1, um valor que se tornará negligenciável à medida que o numero total de colisões aumenta.      

Assim sendo,
```math
\begin{bmatrix} u_2 \\ v_2  \end{bmatrix} = \left(\frac{1}{1+\alpha^2}\right) \begin{bmatrix} 1-\alpha^2 & -2 \\ 2\alpha^2 & 1-\alpha^2  \end{bmatrix}\begin{bmatrix} u_0 \\ v_0  \end{bmatrix}
```

Se o resultado acima já representa necessariamente o resultado de duas colições, vamos definir aqui $k$ positivo para representar o PAR de colisões de modo que possamos afirmar

```math
\tag{4}\begin{bmatrix} u_k \\ v_k  \end{bmatrix} = \left(\frac{1}{1+\alpha^2}\right)^k \underbrace{\begin{bmatrix} 1-\alpha^2 & -2 \\ 2\alpha^2 & 1-\alpha^2  \end{bmatrix}^k}_{C^k}\begin{bmatrix} u_0 \\ v_0  \end{bmatrix},
```

em que $C$ sintetiza a transformação que representa o par de colisões. 

Notemos que k = 1 significa o total de duas colisões, uma relativa à colisão M-m e outra relativa à colisão m-parede; portanto, para dado k, há 2k colisões.  

### A última Colisão
Não haverá mais colisão quando $u_k$ e $v_k$ forem positivos de modo que o bloco 'm' não alcance o bloco 'M', ou melhor: $v_k$ > $u_k$. Limitando-nos a essa condição, a conservação de energia nos fornece

```math
\frac{mu_k^2}{2} + \frac{Mv_k^2}{2} = \frac{MV_{0}^2}{2} \rightarrow v_k = V_0\sqrt{1 - \frac{m}{M}\frac{u_k^2}{V_0^2}}.
```
Se $M >> m$ e  $u_k^2 < V_0^2$, $v_k/V_0$ tenderá a um pela esquerda: $v_k/V_0 \rightarrow 1^-$. Similarmente, complementa-se que $u_k$ tenderá a 0 pela direita, ou melhor: $u_k \rightarrow 0^+$. 

#### Mas vamos explorá-la mais um pouco...

Conseguimos imaginar que suscessivas colisões irão implicar na transferência de energia cinética do bloco maior para o bloco menor. Assim, em algum instante, o bloco maior irá praticamente parar, espremendo o bloco menor entre o bloco maior e a parede, e então terá sua velocidade invertida, que passa a ser positiva. Colisões entre os blocos levarão, agora, ao aumento da velocidade $v_k$ e redução da velocidade $u_k$. 

Logo após a inversão, as colisões ocorrerão com velocidades $u_k >> v_k > 0$, e as colisões subsequentes só irão cessar quando o sistema experimentar $v_k > u_k$, o bloco maior escapará do bloco menor e não haverá mais colisão. 

##### Agora que $`v_k`$ é positivo, qual o sinal de $`u_{k+1}`$ após colisões entre os blocos? 
De acordo com equação (2), o sinal de $u_{k+1}$ será negativo enquanto $u_k > [2/(1-\alpha^2)]v_k $. Esse resultado, consequentemente, implica em mais uma colisão com a parede.

Em seguida, suscessivas colisões reduzirâo $|u_k|$ até que o sistema experimente as velocidades $u_k<[2/(1-\alpha^2)]v_k$, e $u_{k+1}$ venha a ser positivo e menor que $v_{k+1}$, cessando as colisões.

Esse é um indicativo de que a última colisão é do tipo m-M, e que nossos cálculos estão superestimando as colisões em +1. Vamos continuar.   
 
### E agora, qual o valor de k quando as condições finais são alcançadas?
Para responder isso, vamos avaliar como $u_k$ e $v_k$ se comportam com relação a $k$. 

Inicialmente, vamos usar da autodecomposição para calcular $C^k$: $C$ pode ser reeescrito como $C = Q \Lambda Q^{-1}$ em que $Q$ é a matriz de autovetores de $C$, e $\Lambda$ é a matriz diagonal cujos elementos são preenchidos pelos autovalores de $C$.

E por que usar isso? Porque podemos reescrever

```math
C^k = \underbrace{Q \Lambda Q^{-1} ... Q \Lambda Q^{-1}}_{k \times} = Q \Lambda^{k}Q^{-1}
``` 
desde que
```math
QQ^{-1} = I
```

#### Então, vamos achar $`\Lambda`$ e $`Q`$!

##### Encontrando $\Lambda$:

```math
det(C-\lambda I) =  [(1-\alpha^2)-\lambda]^2 + 4\alpha^2 = 0`
```
e aqui nós encontramos dois autovalores complexos:\
$\lambda_1 = (1-\alpha^2) - i2\alpha$ e \
$\lambda_2 = (1-\alpha^2) + i2\alpha$. 

```math
\Lambda = \begin{bmatrix} \lambda_1 & 0 \\ 0 & \lambda_2  \end{bmatrix}
```
##### Encontrando $Q$:

Já os autovetores $v$ são tais que 

```math
(C - \lambda_i I)\begin{bmatrix} x_i \\ y_i  \end{bmatrix} = 0,
```
que nos leva aos autovetores
$`\nu{_1}^T = [1,i\alpha]$ e $\nu{_2}^T = [1,-i\alpha]`$. Portanto:
```math
Q = \begin{bmatrix} 1 & 1 \\ ia & -ia  \end{bmatrix}
```

##### Encontrando $`Q^{-1}`$:

```math
Q^{-1} = \frac{1}{det(Q)}\begin{bmatrix} -i\alpha & -1 \\ -i\alpha & 1  \end{bmatrix} = \frac{i}{2\alpha}\begin{bmatrix} -i\alpha & -1 \\ -i\alpha & 1  \end{bmatrix}.
```
Logo,

```math
Q^{-1} = \begin{bmatrix} \frac{1}{2} & \frac{-i}{2\alpha} \\ \frac{1}{2} & \frac{i}{2\alpha} \end{bmatrix}
```

É possível provar que $QQ^{-1} = I$. 

Por fim, chegamos a
```math
C^k = \begin{bmatrix} 1 & 1 \\ ia & -ia  \end{bmatrix} \begin{bmatrix} \lambda_1^k & 0 \\ 0 & \lambda_2^k  \end{bmatrix} \begin{bmatrix} \frac{1}{2} & \frac{-i}{2\alpha} \\ \frac{1}{2} & \frac{i}{2\alpha} \end{bmatrix}
``` 

Matrizes diagonais, como $\Lambda^k$ atuam como transformações de escala, alterando o comprimento dos componentes dos vetores em que são aplicadas. No nosso caso, em que esses fatores de escala são números complexos, estamos lidando com algo cíclico, uma abordagem que será explorada na **Solução 2** ao fim.  


### Calculando as velocidades $`u_k`$ e $`u_k`$
Conhecendo a equação 4, vamos aplicar o operador $C^k$ sobre as velocidades iniciais $u_0=0$ e $v_0$ = -V$_0$:

```math
\begin{bmatrix} u_k \\ v_k  \end{bmatrix} = \left(\frac{1}{1+\alpha^2}\right)^k \begin{bmatrix} 1 & 1 \\ ia & -ia  \end{bmatrix} \begin{bmatrix} \lambda_1^k & 0 \\ 0 & \lambda_2^k  \end{bmatrix} \begin{bmatrix} \frac{1}{2} & \frac{-i}{2\alpha} \\ \frac{1}{2} & \frac{i}{2\alpha} \end{bmatrix} \begin{bmatrix} 0 \\ -V_0  \end{bmatrix}.
```

```math
\begin{bmatrix} u_k \\ v_k  \end{bmatrix} = \left(\frac{V_0}{2\alpha}\right) \left(\frac{1}{1+\alpha^2}\right)^k \begin{bmatrix} 1 & 1 \\ ia & -ia  \end{bmatrix} \begin{bmatrix} i\lambda_1^k  \\ -i\lambda_2^k \end{bmatrix}.
```

```math
\tag{5}\begin{bmatrix} u_k \\ v_k  \end{bmatrix} = \left(\frac{V_0}{2\alpha}\right) \left(\frac{1}{1+\alpha^2}\right)^k \begin{bmatrix} i(\lambda_2^k-\lambda_1^k) \\ -a(\lambda_1^k + \lambda_2^k) \end{bmatrix}
```

#### Legal, mas o que fazer com $`\lambda_1^k`$ e  $`\lambda_2^k`$?

Vamos utilizar a forma exponencial para expressar esses números complexos:\
$\lambda_1 = (1-\alpha^2) - i2\alpha$ pode ser reescritod como \
$\lambda_1 = re^{i\theta_1}$ tal que $r = \sqrt{ (1-\alpha^2)^2 + (2\alpha)^2 }(= 1+\alpha^2$) e 
$\theta_1 = arctan\left(\frac{-2\alpha}{1-\alpha^2}\right)$.

Analogamente,
$\lambda_2 = (1+\alpha^2)e^{i\theta_2}$ tal que $\theta_2 = arctan\left(\frac{+2\alpha}{1-\alpha^2}\right)$.

Se nos limitarmos ao limite em que $\alpha << 1$, ou M >> m, podemos assumir que $\arctan\left(\frac{-2\alpha}{1-\alpha^2}\right)$ se aproxima de $\frac{-2\alpha}{1-\alpha^2}$, simplificando consideravalemente nossos cálculos, já que chegamos a conveniente situação em que $\theta_1 = - \theta_2$. Assim sendo,

i) $`i(\lambda_2^k-\lambda_1^k) = i(1+\alpha^2)\underbrace{(e^{-ik\theta_2} - e^{+ik\theta_2})}_{=-2isin(k\theta_2)}`$ 
$`= 2(1+\alpha^2)sin(k\theta_2) = 2(1+\alpha^2)sin\left(k\frac{2\alpha}{1-\alpha^2}\right).`$ Também,

ii)$`-a(\lambda_1^k+\lambda_2^k) = -a(1+\alpha^2)\underbrace{(e^{-ik\theta_2} + e^{+ik\theta_2})}_{=2cos(k\theta_2)}`$ 
$`= -2a(1+\alpha^2)cos\left(k\frac{2\alpha}{1-\alpha^2}\right).`$ 

Por fim, chegamos a

```math
\tag{6}\begin{bmatrix} u_k \\ v_k  \end{bmatrix} =  V_0 \left(\frac{1}{1+\alpha^2}\right)^{k-1} \begin{bmatrix} sin\left(k\frac{2\alpha}{1-\alpha^2}\right)/ \alpha \\ -cos\left(k\frac{2\alpha}{1-\alpha^2}\right) \end{bmatrix}
```

### Já podemos identificar k máximo?
Já sabemos que o número de pares de colisões 'k' é tal que antecede o estado em que $v_k \rightarrow V_0^-$ e $u_k \rightarrow 0^+$. Ainda explorando esses limites para o caso em que $\alpha \rightarrow 0$, da equação 6 chegamos a

```math
\tag{7}\begin{bmatrix} u_k \\ v_k  \end{bmatrix} \approx  V_0 \begin{bmatrix} sin(2k\alpha)/\alpha \\ - cos(2k\alpha) \end{bmatrix}
```


#### Esse resultado faz sentido?

```math
\frac{mu_k^2}{2} + \frac{Mv_k^2}{2} = \frac{mV_0^2sin^2(2k\alpha)}{2\alpha^2} + \frac{MV_0^2cos^2(2k\alpha)}{2}
```


```math
\frac{MV_0^2}{2}\left[ sin^2(2k\alpha) + cos^2(2k\alpha) \right] = \frac{MV_0^2}{2}
```

#### por fim...
se a velocidade $v_k \rightarrow V_0^-$, a equação (7) nos mostra que $2k\alpha$ deve tender a  $(2m+1)\pi^-$ tal que $m=0,1,...$ 

Embora nossa abordagem tenha nos apresentado a uma solução cíclica, estamos interessando unicamente no primeiro valor de $m=0$, e neste caso: $2k\alpha \rightarrow \pi^-$. Relembrando que $2k$ representa o número total de colisões, vamos definir $n_c=2k$ para chegarmos a 

```math
n_c \rightarrow \frac{\pi^-}{\alpha}
```

**Logo, podemos verificar que o numero de colisões totais é tal que $n_c \alpha \rightarrow \pi$**

### Podemos explorar mais um pouco... 

Quando assumimos $\alpha$ tão pequeno que a diferença [$`(n_c+2)\alpha - n_c\alpha`$ ] se torna pequeno o suficiente para considerarmos $n_c\alpha$ contínuo, as velocidades $u_k$ e $v_k$ se tornam diferenciáveis com relação a $n_c$, e assim temos da equação (7) que 
```math
du/dn_c \propto -v \tag{8.1}
```
```math
dv/dn_c \propto u, \tag{8.2}
```

e isso faz todo sentido! 

Nos momento iniciais, enquanto $v$ é negativo (indo a esquerda), cada colisão entre os blocos leva ao aumento de $|u|$, que retorna em direção ao bloco de massa M com velocidade cada vez maior, mas ao custo da redução de $|v|$, que praticamente para. 

Contudo, quando $v$ passa a ser positivo, a velocidade $u$ experimenta sua primeira redução em magnitude, enquanto $v$ aumenta ao custo da redução de $|u|$. Eventualmente, o sistema esperimentará $u$ e $v$ positivos, $v$ será maior que $u$ e o sistema nao verá mais nenhuma colisão. 

#### Como chegar nas relações 8?

Primeiro, vamos tornar nossas velocidades diferenciáveis com relação ao número de colisões para que tudo fique mais fácil. Sabemos que o número de colisões é discreto, contudo, no limite em que $M>>m$ o processo de transferência de energia ocorre muito gradualmente, de moddo que possamos assumir que as velocidades variam praticamente continuamente. 

Partindo disso, podemos derivar, com relação o número de colisões, a equação de energia cinética total, que deve ser constante para chegarmos a
```math
mu\frac{du}{dn_c} + Mv\frac{dv}{dn_c} = 0,\,\textrm{ou}
```
```math
\frac{dv}{dn_c} = -\alpha^2\frac{u}{v}\frac{du}{dn_c}\tag{9}
```

Vamos assumir inocentemente que 
```math
\frac{dv}{dn_c} = \alpha^2u \textrm{, e}\tag{10.1}
```

```math
\frac{du}{dn_c} = -v\tag{10.2}
```

para que a equação (9) seja satisfeita e aqui utilizamos o fato de que $v$ precisa ser negativo para que $u$ aumente. Vamos resolver as equações (10). Inicialmente, podemos afirmar que 
```math
d^2u/dn_c^2 = -\alpha^2u \tag{11}.
```

Devido à aparente ciclicidade em $u$, partimos da solução genérica (e complexa) $u = c_1e^{iwn_c} + c_2e^{-iwn_c}$ e a substituitmos em (11) para chegarmos a 
```math
-w^2(c_1e^{iwn_c} + c_2e^{-iwn_c}) = -\alpha^2(c_1e^{iwn_c} + c_2e^{-iwn_c})\textrm{ e}
```
```math
\alpha^2 = w^2 \rightarrow w = \pm \alpha
```

As condições de contorno:

1. $u(0) = 0$: substituindo na solução genérica, temos $c_1 = - c_2$

2. $v(0) = -V_0$: a partir da solução genérica e da equação (10.2), temos $c_1 = iV_0/(2\alpha)$.

Assim: 

```math
u = \pm i\frac{V_0}{2\alpha}(e^{i \alpha n_c} + e^{-i \alpha n_c}) \textrm{, ou}
```
```math
u = \pm\frac{V_0}{\alpha}sin(\alpha n_c)
```

Desde que a cada par de colisões a velocidade inicial de $u$ aumenta, vamos optar pela solução 

```math
u = +\frac{V_0}{\alpha}sin(\alpha n_c)\tag{12}
```

Similarmente:
```math
v = -V_0cos( \alpha n_c)\tag{13},
```

e novamente chegamos às equações em (7). Notemos que $mu^2/2$ $+$ $Mv^2/2$ fornece $MV_0^2/2$, a energia cinética total.

As equações (12) e (13) retornam às equações em (7), alcançadas a partir das seguintes considerações:

1. $\alpha << 1$, quando $M >> m$,
2. velocidades diferenciáveis com relação a $n_c$, que se torna possível devido à aproximação acima; note que $cos(\alpha n_c)$ tende à continuidade quando $\alpha << 1$,
3. o procedimento se torna mais fácil de se interpretar quando pensamos em pares de colisões, mantendo $u$ sempre positivo; essa interpretação foi utilizada para definir a equação (12), e limita a análise sempre para essa ocasião e
4. as velocidades foram obtidas assumindo múltiplos pares de colisão ente bloco menor e bloco maior, e bloco menor e parede,assim, $u$ representa aqui a velocidade do bloco menor após colisão com a parede e é, portanto, positiva.

#### vamos espremer esses blocos mais um pouquinho...

Veja como a equação (13) se assemelha à equação de um sistema massa-mola simples do tipo $u \propto cos(wt)$! Comparando-os: no nosso caso, $n_c \sim t$ e $w = \sqrt{m/M}$, no simples caso, $w = \sqrt{k/M}$.

Assim sendo, podemos pensar que durante o intervalo em que o bloco maior está colidindo com o bloco menor, seu movimento é equivalente a de um sistema massa-mola cuja constante de mola $k$ é equivalente à massa $m$ do bloco menor! 

Podemos definir, então, uma posição arbitrária $x'$ tal que 
```math
kx'^2/2 + Mv^2/2 = E_{Total} = MV_0^2/2 \textrm{,}
```

ou melhor:
```math
mx'^2/2 + Mv^2/2 = MV_0^2/2.
```

Por coveniência, vamos assumir que a relação acima é satisfeita com $x'=-u$, com $u$ positivo, e $x'$ pode ser interpretado com sendo o deslocamento da mola contraída, que adiquire energia potencial enquanto o bloco maior "espreme" o bloco menor contra a parede.   

Oras, se $F = Mdv/dt$ e $F=-kx$ tal que $k=m$. Então,  
```math
dv/dt = \alpha^2u,
```
como a equação (10.1).

Assim, quando $M>>m$ o sistema é comparável a um sistema massa-mola com constante de mola $k=m$, e de alguma forma podemos estimar a posição do bloco maior a partir da velocidade do bloco menor. Se faz importante notar que a comparação com o sistema massa mola foi alcançada assumindo $M>>m$ e só ocorre durante o intervalo em que há colisão entre os blocos, de modo que $u$, ou $x'$, não irão exprimentar senoides inteiras.  

# Solução Segunda

A solução anterior nos apresentou à matrix $C$ que sintetiza a transformação causada por duas colisões sucessivas no sistema: uma entre os blocos m e M, e q seguinte, entre o bloco m e a parede. Essa simplificação é útil uma vez que essas colisões sempre acontecem aos pares quando $M>m$. 

Ainda vimos que a transformação $C$ apresenta autovalores complexos, muito útil na representação de sistemas cíclicos. Vamos explorar esse resultado! 

Segundo o teorema das matrizes "Scaling-Rotating", uma matriz $2\times 2$ que possui auto valores complexos pode ser reescrita na forma $C = PRP^{-1}$ em que $R$ é a incrível representação de uma matriz de rotação com ângulo definidos pelos autovalores de $C$. Ainda, se a norma desses autovalores for diferente de 1, $R$ se torna uma matriz de escala e rotação onde quer que opere.

Se $\lambda_1 = a + ib$, a matriz $R$ é dada simplesmente por: 
```math
R = \begin{bmatrix} a & -b \\ b & a \end{bmatrix},
```

enquanto $P$, a matriz que permite relacionar $C$ com uma matriz de rotação é definida por
```math
P =\begin{bmatrix} | & |\\Re(\nu_1)&-Im(\nu_1) \\  | & | \end{bmatrix}
```

onde deve-se optar por apenas um dos autovalores $\lambda_i$ e autovetor $\nu_i$. Sendo assim, para o nosso caso $\lambda = (1+\alpha^2) - i2\alpha$, e $\nu^T = [1, i\alpha]$ :

```math
C = \frac{1}{1+\alpha^2} \begin{bmatrix} 1 & 0 \\ 0 & -\alpha \end{bmatrix} \begin{bmatrix} 1-\alpha^2 & -2\alpha \\ 2\alpha & 1-\alpha^2 \end{bmatrix} \begin{bmatrix} 1 & 0 \\ 0 & -1/\alpha \end{bmatrix}
```

```math
= \begin{bmatrix} 1 & 0 \\ 0 & -\alpha \end{bmatrix} \begin{bmatrix} cos(\theta) & -sin(\theta) \\ sin(\theta) & cos(\theta) \end{bmatrix} \begin{bmatrix} 1 & 0 \\ 0 & -1/\alpha \end{bmatrix},
```

tal que $\theta = arctan (-2\alpha/(1-\alpha^2))$ e portanto:

```math
 C^k = \begin{bmatrix} 1 & 0 \\ 0 & -\alpha \end{bmatrix} \begin{bmatrix} cos(\theta) & -sin(\theta) \\ sin(\theta) & cos(\theta) \end{bmatrix}^k \begin{bmatrix} 1 & 0 \\ 0 & -1/\alpha \end{bmatrix}.
 ```

Aqui temos um resultado muito interessante: as colisões representadas por $C^k$ representam $k$ suscessivas rotações de ângulo $\theta$ no espaço $u-v$. 

Assim,

```math
 \begin{bmatrix} u_k \\ v_k  \end{bmatrix}  = \begin{bmatrix} 1 & 0 \\ 0 & -\alpha \end{bmatrix} \begin{bmatrix} cos(\theta) & -sin(\theta) \\ sin(\theta) & cos(\theta) \end{bmatrix}^k \begin{bmatrix} 1 & 0 \\ 0 & -1/\alpha \end{bmatrix} \begin{bmatrix} u_0 \\ v_0  \end{bmatrix}\tag{14}.
 ```

Ou

```math
 \begin{bmatrix} u_k \\ v_k  \end{bmatrix}  = \begin{bmatrix} 1 & 0 \\ 0 & -\alpha \end{bmatrix} \begin{bmatrix} cos(\theta) & -sin(\theta) \\ sin(\theta) & cos(\theta) \end{bmatrix}^k  \begin{bmatrix} 0 \\ V_0/\alpha  \end{bmatrix}.
 ```


Sabemos que o processo de colisões se inicia com $[u_0,v_0] = [0,-V_0]$ e tem seu fim quando $[u_0,v_0] \rightarrow [0^-,+V_0^-]$, implicando em uma rotação de aproximadamente $-\pi$ no espaço definido pelas duas velocidades. A partir da equação (14) vemos que cada par de colisões rotaciona o vetor $[u,v]$ em um ângulo $\theta$ de aproximadamente $-2\alpha,$ particularmente válido quando $M>>m$.

Portanto, podemos descobrir o número total de colisões nos perguntando: quantos  $-\alpha$ cabem em $-\pi$? A resposta:

```math
n_c = \frac{\pi^-}{\alpha},
```
o número total de colisoes.

# Gráficos das Soluções
Em resumo, as soluções discutidas são:
- solução analítica, da equação (4), adotada aqui como solução de referência por partir dos princípios mais básicos;
- manipulação da solução analítica, equação (5), alcançada a partir da autodecomposição da matriz de transformação $C^k$ associada ao processo de colisões;
- aproximação da solução anterior, ver equação (6), obtida no limite em que $M>>m$ e
- por fim, a solução que parte que da decomposição da matriz de transformação em subtransformações de escala e rotação, alcançada devido aos autovalores complexos da transformação.

A partir das soluções, as comparações a seguir foram feitas.

## Comparação entre as Soluções

As figuras (1) e (2) mostram, a esquerda, as velocidade $u_k$ e $v_k$ calculada para vários valores de $k$ assumindo o valor fixo de $\alpha = 10^{-2}$. À direita das figuras, são plotados os desvios das velocidades calculadas com relação à solução analítica. Nota-se que a solução aproximada é a que mais se destingue das demais. 

Percebemos que iniciamente as colisões levam a redução  $|v_k|$ e aumento $u_k$, e que  $u_k$ alcança seu máximo quando $v_k$ é nulo.

Aqui, $u_k$ é sempre a velocidade do bloco menor após se colidir com a parede. Portanto, a velocidade negativa vista após $2k>314$ não tem significado físico, etem origem na solução utilizada. 

![Velocity_u](https://raw.githubusercontent.com/matos-pedro/pi_collisions/main/images/u.png)
*Figura 1: esquerda: velocidade $`u_k`$, do bloco menor, calculada a partir das soluções apresentadas; direita: desvio da velocidade calculada com relação à solução analítica.*

![Velocity_v](https://raw.githubusercontent.com/matos-pedro/pi_collisions/main/images/v.png)
*Figura 2: esquerda: velocidade $`v_k`$, do bloco maior, calculada a partir das soluções apresentadas; direita: desvio da velocidade calculada com relação à solução analítica.*

A figura 3 mostra a evolução do vetor velocidade [$`v_k`$,$`u_k`$] após cada par de colisão m-M e m-wall para um valor de $\alpha = 10^{-1}$. A primeira posição corresponde ao valor [-1,0] e a evolução do par de velocidades ocorre no sentido horário, com incrementos de $`\theta = 2\alpha/(1+\alpha^2)`$. Note a discrepância da velocidade aproximada com relação às demais. 

![Arco](https://raw.githubusercontent.com/matos-pedro/pi_collisions/main/images/arco2.png) 
*Figura 3: evolução do vetor [$`v_k`$,$`u_k`$].*

Por fim, $\pi$ é calculado a partir do número total de colisões, aqui definido como $\pi_c$, e é comparado com o valor de $\pi$ definido pela biblioteca numpy, aqui definido simplesmente como 'numpy.pi'. Os resutlados obtidos são apresentados na figura (4) para $\alpha$ variando de $10^{-0.5}$ a $10^{-4}$. 

Os resultados à esquerda representam a razão $`\pi_c`$/numpy.pi, que se aproxima de 1 à medida que $`\alpha`$ se torna mais próximo de 0.

À direita, vê-se o desvio entre os valores calculados e de referência e que seu valor é de aproximadamente $`\alpha`$ : $`\Delta \pi \approx \alpha`$ .

![pi_error](https://raw.githubusercontent.com/matos-pedro/pi_collisions/main/images/pi_1.png)
*Figura 4: cálculo de $`\pi`$; a esquerda, a razão $`\pi_c`$/numpy.pi; a direita, o desvio (numpy.pi - $`\pi_c`$)*

Sendo assim, podemos estimar $`\pi`$ e definir sua precisão a partir de $`\alpha`$.

Fim!
