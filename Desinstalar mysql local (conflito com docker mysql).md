https://tipslegais10.blogspot.com/2013/01/desinstalar-mysql-no-linux-por-completo.html

Primeiro passo é verificar se está instalado o programa com o seguinte comando:

  
**dpkg -l mysql-server**  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiE0tYKsgFO8EBDnb_MV2iJ2YJ1CJyBNer7SpmAHGpFuzDuBG4mTAwrxxXyvDnYpsC5X80gBnxiAhkMzA05-IoKcNaPpiC50kZ2R_qhphsD2Uk7qr-rsfFME0-qKdsIZPPmkV1IA3RmFus/s400/12.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiE0tYKsgFO8EBDnb_MV2iJ2YJ1CJyBNer7SpmAHGpFuzDuBG4mTAwrxxXyvDnYpsC5X80gBnxiAhkMzA05-IoKcNaPpiC50kZ2R_qhphsD2Uk7qr-rsfFME0-qKdsIZPPmkV1IA3RmFus/s1600/12.jpg)

  
  
Como podemos ver o resultado do comando, o pacote esta com "**ii**" no começo da linha, significa que o pacote está instalado.  

  

Para remover completamente o SGBD (Sistema de Gerenciamento de Banco de Dados), sem deixar rastro execute as seguintes linhas de comando no terminal.

  
Acesse o terminal e digite:  
  
**sudo apt-get remove --purge mysql-server**  
  
  
Próximo passo remover o PHPMYADMIN - gerenciador gráfico de banco de dados.  
  
**sudo apt-get remove** **--purge** **phpmyadmin**   
  
Vai aparecer duas telas a seguir selecione a opção **_sim_** quando elas aparecerem vai pedir a senha do administrador do banco coloque a senha e confirme.  
  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgSo64JfhIGbPdZmxy8FxvO7s_v27XFUW8XL_NVaxonO25I6NKb6-vpNaY_bja9umFVOMkYQB_3OblZ4F9Virlo65Y7sT30rr4Pdvz4NNxYyiylvdkoRkV-VtcbprggIdvgU8RJeRTATP4/s400/15.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgSo64JfhIGbPdZmxy8FxvO7s_v27XFUW8XL_NVaxonO25I6NKb6-vpNaY_bja9umFVOMkYQB_3OblZ4F9Virlo65Y7sT30rr4Pdvz4NNxYyiylvdkoRkV-VtcbprggIdvgU8RJeRTATP4/s1600/15.jpg)

  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgQ0MfZ4gySh3ltfyO_eKn-vJdcHx8mek-MqocghyphenhyphenAiblyvroceNHdH8Myo-_uPJOpXd3vIbWCfgXPoWfKOvlp-gXkd1PBhSjQOvpC0WcrS9cBS4SNlfzVcGfndklZ4s2UiXKxixpc4ed0/s400/14.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgQ0MfZ4gySh3ltfyO_eKn-vJdcHx8mek-MqocghyphenhyphenAiblyvroceNHdH8Myo-_uPJOpXd3vIbWCfgXPoWfKOvlp-gXkd1PBhSjQOvpC0WcrS9cBS4SNlfzVcGfndklZ4s2UiXKxixpc4ed0/s1600/14.jpg)

  
  
  
Vamos parar o serviço do MySQL.  
  
**sudo /etc/init.d/mysql stop**  
  
Agora vamos remover mais um pacote do MySQL.  
  
**sudo apt-get remove --purge mysql-common**  
  

  
  

Por ultimo apague a pasta **mysql** que fica localizada em /var/lib/ com o comando abaixo e pressione enter:

  

**sudo rm -rf /var/lib/mysql**

  
  
  
Depois de fazer todos os passos acima digite um comando de cada vez no terminal:

1. **sudo apt-get autoremove --purge**
2. **sudo apt-get autoclean**
3. **sudo apt-get clean**

  

Verificando novamente se o _MySQL_ está instalado.