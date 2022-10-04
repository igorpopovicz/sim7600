<h1 align="center">
  <img src="public/simcard.png" width="100">
  <br>
    Sim7600-MT7688
</h1>
<p>Integrating the Qualcomm-Sim7600SA modem (3g / 4g) into a hi-link MT7688 (running Open-WRT)</p>
(☝️ in firmware has a ready image, with the necessary packages already installed and the network already updated.)
<br>
<br>

## Prerequisites :
- Qualcomm-Sim7600XX. 
- hlk-mt76x8. 
- Open-WRT image builder SKD. 
- PC linux.

## Verifying that everything is prepared :
Make sure your Open-WRT image has the following packages ->
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

After compiling the image (or installing the packages) start MT7688 with Sim7600 on the USB port

With the dmesg command, check if the module started correctly ->
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
If no errors were reported, we can continue :)

## Configuring the wwan connection
Now that Sim7600 is integrated with MT7688 we can configure the wwan parameters ->
```
cd ..
```
```
cd etc/config
```
Using nano (or any other text editor) add the following configuration to the network file ->
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
on
<br>
- 1
```
        option pincode XXXX
```
"XXXX" is the pin password of the chip being used
<br>
<strong> 
This part is not mandatory, only add it if necessary
</strong>
<br>
- 2
```
        option apn     claro.com.br
```
<strong>
Change "claro.com.br" to your mobile carrier's apn
</strong>
<br>
<br>

- 3 

```
        option service ip 
```
<strong> 
"ip" is the umts (Universal Mobile Telecommunications System) that your operator uses | IP | PPP | IPv6 | IPv4v6 |
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

 If you follow these steps, this integration should work. Hope this helps :)
 <br>
 by Popovicz. ͡•_ゝ ͡•




