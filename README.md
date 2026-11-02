# minha primeira LLM

Queria entender de verdade como um modelo de linguagem funciona por dentro, então resolvi montar um do zero.

Comecei pelo básico (como transformar texto em número) e terminei treinando um RoBERTa com o livro *Crepúsculo dos Ídolos*, do Nietzsche. O tokenizer e o modelo começam sem saber nada e aprendem só com esse livro.

Tudo está no notebook [`Minha_primeiraLLM.ipynb`](Minha_primeiraLLM.ipynb).

## o que tem no notebook

1. uma "cifra" que transforma letra em número (e quebra quando aparece letra que ela nunca viu)
2. one-hot com palavras inteiras, e por que isso não escala
3. tokens com o `tiktoken` do GPT-2, que picota o português bem mais que o inglês
4. a diferença entre o jogo do GPT (próxima palavra) e o do BERT (preencher lacuna)
5. um tokenizer Byte-Level BPE treinado com o livro
6. um RoBERTa pequeno treinado do zero, rodando no meu PC sem GPU
7. testes com `<mask>` pra ver o que ele aprendeu

## como ficou

Modelo com 4,5 milhões de parâmetros, treinado 300 épocas no CPU (14 min + 25 min). O loss foi de 5.6 pra 1.3.

Ele ainda erra muito, mas já dá pra ver o livro nos chutes:

```
a moral é uma invenção dos <mask>.
   crimin          20.1%     (de criminoso, que aparece várias vezes no livro)
   organizadora    9.9%
```

Na frase que está no livro ("o que não me faz morrer me torna mais forte") ele não acertou o "forte". Um livro só é pouco texto, e o modelo é bem pequeno.

## como rodar

Python 3 e Jupyter. As instalações estão nas próprias células (`%pip install ...`), é só rodar de cima pra baixo. O livro é baixado sozinho.

## créditos

Segui a aula [LLM na Prática](https://www.youtube.com/watch?v=LphBQB1amrw) do Prof. Marlon Ferrari ([repo original](https://github.com/ferrarimarlon/NietzscheLLM)) e adaptei algumas coisas: modelo menor pra caber no CPU, menos épocas, o livro inteiro cortado em blocos em vez de linha por linha e o teste do `<mask>` montado na mão em vez do `pipeline`.
