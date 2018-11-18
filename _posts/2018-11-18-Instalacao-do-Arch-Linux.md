---
title: "Instalação do Arch linux"
author: "Nilsonlinux"
output:
 html_document:
   toc: true
 github_document:
   always_allow_html: yes
   toc: true
categories: Instalação Linux
layout: post
featured_image: /images/linux/como-instalar-archlinux.jpg
---



## Instalação do ArchLinux ##
Para procederem à instalação do ArchLinux devem seguir os seguinte passos:

Passo 1) Depois de fazer boot com o sistema, deverá escolher a opção Boot Arch Linux (x86_64).  



 

Passo 2) Depois de fazer boot e entrem na shell e executem o comando fdisk –l para verem o espaço em disco e esquema de partições (caso existam).

No nosso caso, temos disponível um disco de 8 GB. Para criar as partições necessárias, devem executar o comando cfdisk



**Particionamento do sistema**  
Passo 3) Para a elaboração deste tutorial, tendo em conta que temos um disco de 8 GB, vamos considerar o seguinte esquema de partições:

Partição Root: 6 GB
Partição Swap: 2 GB
Para criarem a partição Root, devem escolher>New e Primary. Devem também indicar que essa partição é Bootable.



No espaço que resta vamos criar a partição swap, carregando também em New, depois escolher extended.



Em seguida voltamos a carregar em New e no Type escolher a opção 82 Linux swap/Solaris.



O esquema de partições criado deverá ficar idêntico ao apresentado na seguinte imagem.



**Formatar partições**
Passo 4) Vamos agora proceder à formatação das partições root e swap. Para isso basta que usem os seguintes comandos:

```mkfs.ext4 /dev/sda1```  
Para formatar e inicializar a partição swap, basta que executem os seguintes comandos:

```mkswap /dev/sda2```  
```swapon /dev/sda2```  
Vamos agora executar o comando lsblk para verificar se está tudo ok.



Instalação do sistema Base
Passo 7) Para iniciar a instalação do sistema, devem executar o seguinte comando. Nota: Durante a instalação, devem escolher as opções por omissão (default=all)

```pacstrap -i /mnt base base-devel```  


Uma vez finalizado o processo de instalação é hora de criar o nosso ficheiro fstab (File System Table), em /mnt/fstab, e que me permitirá informar o sistema quais as partições a mapear durante o arranque do sistema.

Para isso basta que usem o seguinte comando:

```genfstab -U -p /mnt >> /mnt/etc/fstab```  
Configuração base do sistema
Passo 8) Para configurarmos o Arch Linux é necessário recorremos ao chroot – uma forma de isolar aplicações do resto do sistema. Para isso basta executar o comando:

```arch-chroot /mnt```  
Passo 9) O próximo passo é a instalação do idioma. Para isso basta abrir o ficheiro /etc/locale.gen e remover o comentário dos idiomas que pretendemos instalar.

Depois de escolhidos os idiomas e de termos saído do ficheiro executamos o seguinte comando para instalar os idiomas:
```locale-gen```  
Passo 10) Para definir o idioma para PT devem executar o seguinte comando:

```LANG="pt_PT.UTF-8" locale > /etc/locale.conf```  
Passo 11) Relativamente à definição do esquema do teclado, basta que executem o seguinte comando:

```echo "KEYMAP=pt-latin9" > /etc/vconsole.conf```  
Configuração do Fuso Horário

Passo 12) Para definirmos o nosso fuso horário, basta criar um link simbólico para de /usr/share/zoneinfo/Europe/Lisbon para /etc/localtime

```ln -s /usr/share/zoneinfo/Europe/Lisbon /etc/localtime```  
Criação da imagem modular initramfs

Para a criação do Initramfs, ficheiro que aponta para o Kernel Linux (executar certas tarefas antes de o root filesystem ser montado), basta usar a ferramenta mkinitcpio

```mkinitcpio -p linux```  


Instalação do boot
Passo 13) O último passo é a instalação do bootloader para podermos escolher qual o sistema a arrancar. Para instalar o bootloader no primeiro disco (/dev/sda) e detectar automaticamente outros sistemas instalados, basta correr os seguintes comandos:

```pacman -S grub```  
```grub-install /dev/sda```  
```pacman -S os-prober```  
```grub-mkconfig -o /boot/grub/grub.cfg```  
E está feito. Vamos agora sair do ambiente de chroot e desmontar do diretório /mnt/.

```umount /mnt```  
Por fim reiniciamos o sistema
```reboot```  
Iniciar Sistema
Para arrancarem o sistema, basta que escolham Arch Linux OS 

Para entrarem no sistema apenas o utilizador root está disponível. Como não definimos password durante o processo de configuração, basta indicar o username. Depois de entrarem no sistema podem de imediato definir uma password para o utilizador root usando o comando
```passwd```  



Difícil? Um pouco… mas é mais pela quantidade de comandos que temos de usar para proceder à instalação, algo que já não se faz em outras distribuições Linux cujo o assistente de instalação dá uma ajuda preciosa. Alguma dúvida ou questão não hesitem em nos perguntar. Eu super recomendo lê a wiki do arch. Foi de lá que retirei estes comandos. Abraços.

 _By: Nilsonlinux_