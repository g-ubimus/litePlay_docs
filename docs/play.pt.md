# `toque()`

No núcleo do litePlay.js temos o `play()`. Ele pode ser simplesmente executado
como

```
toque();
```

para tocar um som, e `pare()` para pará-lo. Estas linhas de código podem ser
digitadas diretamente em um console REPL interativo ou adicionadas ao script.

Podemos fazer alterações neste som definindo o instrumento padrão que o reproduz,

```
instrumento(órgão);
```

o padrão foi definido como piano no início, mas agora mudamos para organ. Uma
introdução aos instrumentos é dada no final do tutorial.

Também podemos dizer o que tocar. Se o som for de um instrumento afinado
(pitch), podemos pedir para tocar uma determinada nota,

```
toque(E4);
```

Os nomes simbólicos das notas variam de Cm1 (=C<sub>-1</sub>) a G8
(=G<sub>8</sub>), de tal forma que o Dó central de um teclado de piano é
definido como C4. O som é tocado imediatamente e dura indefinidamente (embora
alguns possam decair em intensidade ao longo do tempo).

Acidentes são representados pela letra minúscula `s` para _sustenidos_ (sharp)
e `b` para notas _bemóis_ (flat):

```
toque(Eb4);
toque(Fs4);
```

## Events (Eventos)

No litePlay.js podemos pensar na ação resultante do `play()` desta forma como
um _evento_ musical. Podemos defini-lo com cinco atributos:

* _what_ (o que): a coisa que tocamos, que pode variar, mas no caso mostrado
  anteriormente, é a altura (pitch) do som.
* _howLoud_ (quão forte): o volume do som, que pode ser definido por um valor
  numérico em uma escala de 0 a 1.
* _when_ (quando): o tempo do evento, quando ele deve acontecer, no caso
  presente, definido em segundos.
* _howLong_ (quanto tempo): por quanto tempo o som deve durar, em segundos.
* _onSomething_ (em algo): a coisa que fará o som, o instrumento, como `organ`,
  `violino` etc. Existem vários destes para escolher. Dependendo do tipo de
  instrumento, o que (_what_) pode ser tocado pode variar. Por exemplo, no caso
  da `bateria`, não temos altura, mas sons de percussão
  diferentes como `caixa`, `bumbo`, etc.

Os atributos (ou parâmetros) do evento são opcionais, como já vimos. Se os
passarmos, os padrões serão usados. É possível passar apenas alguns parâmetros,
por exemplo, apenas _what_; _what_ e _howLoud_; _what_, _howLoud_ e _when_; bem
como _what_, _howLoud_, _when_ e _howLong_.

Os eventos são passados usando uma lista JS (ou array) com atributos na ordem
listada anteriormente:

```
[o quê, quão forte, quando, quanto tempo, em algo]
```

Por exemplo,

```
toque([C4, 0.5, 0, 2, violino])
```

A ação `toque()` pode receber vários eventos como argumentos, como

```
toque([C4, 0.1, 0, 3], [E4, 0.2, 0.5, 0.5], [G4, 0.4, 2, 0.1])
```

Agora aprendemos que podemos trabalhar com listas de eventos, em vez de apenas
enviar eventos individuais para o `toque()`. Há um aspecto particular disso que
devemos notar, os atributos _when_ de cada evento serão interpretados de uma
certa maneira.

### Uma lista simples de _what_ (o que)

```
toque(C3, C4, C5);
```

Neste caso, os eventos serão separados pelo _howLong_ padrão para o
_onSomething_ sendo tocado (definido como 1 seg). Assim, ouvimos os sons em
sequência.

### Uma lista de eventos incompletos

```
toque([C3], [C4], [C5]);
```

Neste caso, o padrão para _when_ é 0, imediatamente, para todos os eventos na
lista. Ouvimos os sons começando ao mesmo tempo, misturados.

### Uma lista de eventos com atributos _when_ definidos explicitamente

```
toque([C3, 0.1, 0], [C4, 0.2, 1], [C5, 0.4, 2]);
```

Neste caso, o tempo dos eventos é relativo ao momento em que pedimos para a
lista de eventos ser tocada, com talvez um atraso muito curto. Todos os eventos
são cronometrados com precisão em relação a isso. Podemos decidir quando eles
devem entrar com um tempo exato.

E se uma lista de eventos se tornar um [objeto](./eventList.md)?
