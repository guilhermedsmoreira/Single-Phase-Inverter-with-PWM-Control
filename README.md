# ⚡ Single-Phase Inverter with PWM Control

Este projeto é uma continuação do estudo anterior sobre inversores monofásicos. Agora, o mesmo circuito H-Bridge será analisado com a adição do controle por modulação por largura de pulso (PWM).

---

## 🔧 Componentes do Circuito

O circuito é composto por:

- 4 transistores MOSFET tipo N;
- Fonte de tensão contínua de 5 V;
- Carga resistiva de 10 kΩ;
- Fontes de controle PWM;
- Buffers e amplificadores operacionais.

![Circuito completo](caminho-da-imagem)

---

## 📈 Forma de Onda da Carga

A simulação foi feita no LTspice. Abaixo, é possível observar a forma de onda da tensão sobre a carga resistiva:

![Forma de onda da carga](caminho-da-imagem)

---

## 🎛️ Controle PWM

Para controlar o inversor com PWM, utilizamos:

- 2 comparadores;
- 3 fontes de tensão: `Vp1`, `Vp2` e `Vc`.

![Circuito PWM resumido](caminho-da-imagem)

- `Vp1` e `Vp2` são as portadoras (dente de serra), sendo `Vp2` o inverso de `Vp1`;
- `Vc` é a tensão de controle (constante de 10 V).

O comparador ativa sua saída sempre que `Vc` ultrapassa o valor instantâneo de `Vp1` ou `Vp2`.

---

## 🔁 Amplificador Operacional Inversor (Ganho Unitário)

Para garantir que `Vp1` e `Vp2` tenham o mesmo valor eficaz (Vrms), foi utilizado um amplificador operacional inversor com ganho unitário.

- Resistores utilizados: `R1 = R2 = 10 kΩ`.
- Resultado: inversão da forma de onda sem alterar sua magnitude.

![Amp Op inversor](caminho-da-imagem)

---

## ⚖️ Amplificador Operacional Comparador

A comparação entre `Vc` e as portadoras `Vp1` e `Vp2` é feita por meio de comparadores com amplificadores operacionais.

- Quando `Vc > Vp1` → saída do comparador é alta;
- Quando `Vc < Vp1` → saída do comparador é baixa;
- O mesmo ocorre com `Vp2`.

Este é o princípio da geração dos pulsos PWM utilizados para acionar os MOSFETs do inversor.

![Ondas Vp1, Vp2, Vc](caminho-da-imagem)

---

## 🧱 Buffer

Foi utilizado um buffer (seguidor de tensão) na saída dos comparadores com o objetivo de garantir o isolamento e a integridade dos sinais antes de acionar os MOSFETs.

Esse componente serve para:

- Evitar que o circuito de controle seja afetado pela carga dos MOSFETs;
- Preservar a forma do sinal de controle;
- Proporcionar **alta impedância de entrada** e **baixa impedância de saída**, características fundamentais para acoplamento eficiente entre estágios.

O uso do buffer assegura que os sinais PWM cheguem aos transistores de forma estável e sem distorções.

## 🔍 Queda na Tensão Efetiva (Vrms)

No circuito anterior (sem controle PWM), a tensão eficaz na carga era aproximadamente **5 V**, valor esperado dada a fonte DC de **5 V** e o acionamento direto dos MOSFETs.

Com a introdução do controle **PWM (Pulse Width Modulation)**, a forma de onda da tensão na carga deixou de ser constante e passou a ter pulsos periódicos. Isso significa que a energia média entregue à carga foi reduzida, refletindo diretamente em uma **queda no valor eficaz da tensão (Vrms)**.

Na simulação atual, com o PWM ativo e um período de **16 ms**, a tensão eficaz medida na carga foi de aproximadamente **4.07 V**. Essa diferença ocorre devido ao tempo em que o sinal permanece em nível baixo durante o ciclo (tempo desligado), reduzindo a área sob a curva da tensão ao longo do tempo.

Esse comportamento é esperado e está diretamente relacionado ao **fator de condução** (ou duty cycle) aplicado no PWM. Quanto menor o tempo em que o sinal permanece em nível alto (Ton), **menor será o valor eficaz da tensão** na carga.

> Ou seja, a queda na Vrms é uma consequência natural e controlada do uso do PWM — técnica essencial para ajustar a potência fornecida à carga sem alterar a tensão da fonte.



## 📌 Observações

- O uso da técnica PWM permite controlar a tensão RMS na carga variando o tempo de condução dos MOSFETs;
- Um valor maior de tempo "ligado" (maior duty cycle) resulta em maior tensão RMS na carga;
- O circuito foi simulado utilizando LTspice com uma frequência de comutação de 50 Hz.

---

## 📎 Conclusão

O controle por PWM se mostrou eficaz para modular a tensão de saída do inversor monofásico. O circuito apresentado é uma base importante para o estudo de formas de onda, harmônicos e eficiência de conversão em inversores de potência.


