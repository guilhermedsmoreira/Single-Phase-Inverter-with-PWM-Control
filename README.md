# Single-Phase-Inverter-with-PWM-Control
O mesmo circuito inversor monofásico estudado anteriormente está sendo usado nesse caso. Porém, agora estaremos utilizando o método PWM para controlar nosso circuito.
Dessa forma, o circuito conta com 4 MOSFETS tipo N, uma fonte cc de 5V e a carga uma resistência de 10kohm.
Para compor o circuito de controle PWM, foi também utilizado outros tipos de circuito como o buffer, amplificador operacional com ganho unitário e comparador.
Todos esses artifícios serão detalhados abaixo.

#imagem circuito

#imagem ondas

# Controle PWM
Para construirmos um controle PWM para o circuito inversor, em resumo pode ser utilizado 2 comparadores e 3 fontes tensão: Vp1, Vp2 e Vc.

#imagem circuito resumido

Vp1 e Vp2 são as portadoras e Vc é a tensão de controle.
Dessa forma, o comparador irá sobrepor a onda Vc nas ondas Vp1 e Vp2, e no ponto em que Vc cruzar essas ondas, ele irá ligar ou desligar sua saída.
No circuito construído no LTspice, Vc foi definida com 10Vcc e Vp1 e Vp2 com 24V pico a pico (sendo Vp2 o inverso de Vp1). Nota-se que para inverter a forma de onda de Vp2, foi utilizado o circuito amp op inversor.]
#imagem Vp1Vp2_onda, Vc

# Amplificador Operacional Inversor Unitário

(citar caract gerais) ...
A escolha dos valores de resistorem iguais (Vr1=Vr2=10kohm) foi com o intuito do ganho ser unitário, e assim Vp1 e Vp2 possuírem o mesmo Vpp. Dessa forma, nosso amp op irá inverter a polaridade do sinal mantendo sua magnitude.
