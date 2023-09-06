# Tyni-OS
Projeto para a disciplina de Teste e verificação de software - UFSC

Este projeto tem como base a rede de Petry a seguir:

<img src="/Problema.png" width="400" />

O objetivo do projeto e escrever um modelo correspondente ao do problema em uma ferramenta e elaborar propriedades de safety e liveness

## Desenolvimento

O problema foi modelado em dois programas diferentes: Uppaal e Tapaal.

No Uppaal, a modelagem foi realizada utilizando 3 templates de processos: tarefas, controladores de disco e CPUs. Levando em consideração o tempo e recurso computacional necessários para realizar a verificação das proposições, o sistema foi modelado também no Tappaal.

O Tapaal permite modelar sistemas usando redes de Petry, o que facilitou bastante o trabalho, visto que o problema foi propposto usando rede de Petry

## Proposições

As proposições feitas foram:

    Não há deadlocks no sistema:
        AG (! deadlock) - Sempre, globalmente, não há deadlock.
    Em qualquer estado do sistema, todas as transições podem eventualmente acontecer.
        AG ((EF tinyos.startLoading) and (EF tinyos.endLoading) and (EF tinyos.startUnload) and (EF tinyos.endUnload) and (EF tinyos.freeMemory) and (EF tinyos.startFirst) and (EF tinyos.suspend) and (EF tinyos.startNext))
    Eventualmente, não haverão tarefas no disco.
        EF tinyos.TaskOnDisk = 0
    Eventualmente, todas as tarefas estarão sendo executadas simultaneamente.
        EF tinyos.CPUUnit = 0
    Eventualmente, haverão mais tarefas prontas do que o número de CPUs
        EF (tinyos.CPUUnit = 0 and tinyos.TaskReady != 0)

O resultado dessas proposições podem ser verificados executando os programas.
