# Decisoes da pratica A

Explique, com referencia a uma chamada do programa:

1. Na falta de calibracao, qual funcao lanca, qual apenas propaga e qual recupera a falha? Responda para C++ e Python.
Em C++, quem lanca a FalhaCalibracao e a funcao adquirir, quando a fonte esta disponivel, mas nao esta calibrada. A funcao lerServico apenas chama adquirir e deixa a excecao passar. Depois, a funcao executarCiclo captura essa falha e informa que o motivo foi calibracao.
No Python acontece a mesma coisa: adquirir lanca a excecao, ler_servico apenas propaga e executar_ciclo captura e retorna o resultado com o motivo calibracao.
Isso aparece no make run na mensagem Sem calibracao: sem leitura (calibracao).

2. Por que a captura de `FalhaCalibracao` vem antes da de `FalhaLeitura`? Quando a sessao e liberada em cada linguagem?
A FalhaCalibracao vem antes porque ela e uma especializacao de FalhaLeitura. Se a FalhaLeitura fosse capturada primeiro, a falha de calibracao tambem seria tratada como uma falha comum e perderiamos a informacao de que o problema foi a calibracao.
No C++, a sessao e liberada automaticamente quando o objeto Sessao sai da funcao adquirir, inclusive quando acontece uma excecao. No Python, ela e liberada pelo finally, que executa mesmo quando ocorre uma falha.

3. Como `FonteNivel` e `FonteConstante` podem ser consultadas pelo mesmo contrato? Dê um exemplo observado em `make run`.
As duas fontes seguem a mesma interface IFonteLeitura. Por isso, o programa consegue usar as duas pelo mesmo contrato, mesmo elas tendo implementacoes diferentes.
Um exemplo no make run e a mensagem Fonte simulada: 42.5 %, que vem da FonteConstante, enquanto a leitura Leitura: 20 vem da fonte ligada ao SensorNivel. As duas podem ser usadas pelo mesmo fluxo de leitura.