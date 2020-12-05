<h1 align="center">
  <img src="public/meupau.png" width="100">
  <br>
    Sim7600-MT7688
</h1>
<p>Integrando o modem Qualcomm-Sim7600SA (3g/4g) em um MT7688 da hi-link (rodando Open-WRT)</p>
<br>

## Pré requisitos :
- Qualcomm-Sim7600XX. 
- hlk-mt76x8. 
- Open-WRT image builder SKD. 
- PC linux.

## Verificando se está tudo preparado :
Certifique-se que sua imagem Open-WRT tem os seguintes pacotes ->
- comgt
- kmod-usb2
- kmod-usb-ohci
- kmod-usb-uhci
- kmod-usb-serial
- kmod-usb-serial-option
- kmod-usb-serial-wwan
- kmod-usb-acm
- modeswitching
- usb-modeswitch
- kmod-usb-core
- chat
- ppp
- kmod-usb-serial

Após compilar a imagem (ou instalar os pacotes) inicie o MT7688 com o Sim7600 na porta USB

Com o comando dmesg observe se o módulo foi iniciado corretamente ->
```
[   18.991545] usbcore: registered new interface driver usbserial_generic
[   19.004673] usbserial: USB Serial support registered for generic
[   19.075957] xt_time: kernel timezone is -0000
[   19.102394] usbcore: registered new interface driver cdc_ncm
[   19.274119] urngd: v1.0.2 started.
[   19.366477] mt76_wmac 10300000.wmac: ASIC revision: 76280001
[   19.536733] random: crng init done
[   19.543503] random: 1 urandom warning(s) missed due to ratelimiting
[   20.416327] mt76_wmac 10300000.wmac: Firmware Version: 20151201
[   20.428132] mt76_wmac 10300000.wmac: Build Time: 20151201183641
[   20.486178] mt76_wmac 10300000.wmac: firmware init done
[   20.680438] ieee80211 phy0: Selected rate control algorithm 'minstrel_ht'
[   20.882222] PPP generic driver version 2.4.2
[   20.906422] NET: Registered protocol family 24
[   20.932497] qmi_wwan 1-1:1.5: cdc-wdm0: USB WDM device
[   20.955047] qmi_wwan 1-1:1.5 wwan0: register 'qmi_wwan' at usb-101c0000.ehci-1, WWAN/QMI device, aa:9e:4e:29:04:e0
[   20.975861] usbcore: registered new interface driver qmi_wwan
[   21.078415] usbcore: registered new interface driver cdc_mbim
[   21.126402] usbcore: registered new interface driver option
[   21.137620] usbserial: USB Serial support registered for GSM modem (1-port)
[   21.152171] option 1-1:1.0: GSM modem (1-port) converter detected
[   21.258338] usb 1-1: GSM modem (1-port) converter now attached to ttyUSB0
[   21.272563] option 1-1:1.1: GSM modem (1-port) converter detected
[   21.324144] usb 1-1: GSM modem (1-port) converter now attached to ttyUSB1
[   21.338467] option 1-1:1.2: GSM modem (1-port) converter detected
[   21.414323] usb 1-1: GSM modem (1-port) converter now attached to ttyUSB2
[   21.428548] option 1-1:1.3: GSM modem (1-port) converter detected
[   21.491195] usb 1-1: GSM modem (1-port) converter now attached to ttyUSB3
[   21.505453] option 1-1:1.4: GSM modem (1-port) converter detected
[   21.586391] usb 1-1: GSM modem (1-port) converter now attached to ttyUSB4
[   21.650686] usbcore: registered new interface driver qcserial
[   21.662312] usbserial: USB Serial support registered for Qualcomm USB modem
```
Se nenhum erro foi reportado, podemos continuar :)

## Configurando a conexão wwan
Agora que o Sim7600 está integrado com o MT7688 podemos configurar os parâmetros de wwan ->
```
cd ..
```
```
cd etc/config
```
Usando o nano (ou qualquer outro editor de texto) adcione a seguinte configuração no arquivo network ->
```
nano network | vi network
```
Add
```
config interface wan

        option pincode XXXX
        option device  /dev/ttyUSB2
        option apn     claro.com.br
        option service ip
        option proto   3g
```
Onde
<br>
- 1
```
        option pincode XXXX
```
"XXXX" é o senha pin do chip que está sendo utilizado
<br>
<strong> 
Essa parte não é obrigatória, só adcione se for necessário
</strong>
<br>
- 2
```
        option apn     claro.com.br
```
<strong>
Troque "claro.com.br" pelo apn de sua operadora
</strong>
<br>
<br>

- 3 

```
        option service ip 
```
<strong> 
"ip" é o umts (Universal Mobile Telecommunications System) que sua operadora utiliza |IP|PPP|IPv6|IPv4v6|
</strong>
<br>
<br>

- 4

```
        option proto   3g
```
<strong>
Proto -> 3g/4g
</strong>
<br>
<br>
<br>
<br>

 Se seguir esses passos esssa integração deve funcionar. Espero ter ajudado :)
 <br>
 by Popoviczorigin main




