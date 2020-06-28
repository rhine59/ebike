# Fitting a TongSheng TSDZ2 mid drive motor with an 8 pin controller to a 52v battery and the Bafang 860C LCD

<!-- TOC -->

- [Fitting a TongSheng TSDZ2 mid drive motor with an 8 pin controller to a 52v battery and the Bafang 860C LCD](#fitting-a-tongsheng-tsdz2-mid-drive-motor-with-an-8-pin-controller-to-a-52v-battery-and-the-bafang-860c-lcd)
- [Building a `bootloader` to flash the 860c display](#building-a-bootloader-to-flash-the-860c-display)
  - [Tools you will need](#tools-you-will-need)
  - [Sourcing components](#sourcing-components)
  - [Adjusting the output voltage from the DC Booster](#adjusting-the-output-voltage-from-the-dc-booster)

<!-- /TOC -->

There is not much original content here, I am walking in the footsteps of those who know more than me, but hope that pulling all the threads together that I needed if of help to those who follow. I hope that I have given all the credits and references that are due, but if I have missed anything, then please contact me and I will happily update this content.

I am in no way trying to place product here. Any images or links are provided as samples that illustrate the story and work for me, and there are likely to be other ways to achieve the same result, but this journal is her to chronical my journey.

# Building a `bootloader` to flash the 860c display

## Skills

All you need to do this is a logical mind who can read, think, plan and execute. This is 90% planning and 10% execution.

## Tips

1. Read and understand, don't learn and make mistakes as you go.
2. Think, think again and then cut

## Tools you will need

<p float="left">
  <img src="images/2020/06/multimeter.png" width="100" />
  <img src="images/2020/06/screwdrivers.png" width="100" />
  <img src="images/2020/06/heatshrink.png" width="100" />
  <img src="images/2020/06/male-and-female-wires.png" width="100" />
  <img src="images/2020/06/soldering.png" width="100" />
</p>

- Multimeter - 0 volts to 40 volts DC
- Watch makers screwdriver to adjust output voltage of DC Buck converter
- Heatshrink tubing to provide electrical isolation and assembly strength.
- Wires for connecting components. You will need the female ended connectors, but we do not need the male ends.
- Solder / Flux / Iron - I assume that you have access to this already.

## Sourcing components

Cable colours do not matter here. Just make sure that you use a colour scheme that follows the logic of the recipe. I have used the schematic from [here](https://github.com/OpenSource-EBike-firmware/TSDZ2_wiki/wiki/Flash-the-firmware-on-860C-850C-using-bootloader)

![bootloader schematic](images/2020/06/bootloader-schematic.png) Ignore the voltage `adjust 27V-58.8V` in the diagram. We will be using 30 volts.

Following the recipe [here](https://github.com/OpenSource-EBike-firmware/TSDZ2_wiki/wiki/Flash-the-firmware-on-860C-850C-using-bootloader) and I sourced the following parts.

1. `A CH340G RS232 to USB TTL Auto Converter Adapter` to take the signal from the `APT Burn Tools` updating software and deliver it to the `860c` LCD display.

![USB to TTL converter](images/2020/06/usb-to-ttl-converter.png)

[EBAY Search](https://www.ebay.co.uk/sch/i.html?_from=R40&_trksid=m570.l1313&_nkw=CH340+Gold+USB+TTL&_sacat=0)

2. `A 5 pin Higo Mini A extension cable - male to male`. You will cut this in half, use 1 half to create the bootloader, and the other will attach to the end of the 860c LCD connection to the motor controller.

![Higo Mini A](images/2020/06/higo-mini-a.png)

[Amazon search](https://www.amazon.co.uk/Bafang-Extended-Cable-Display-750C/dp/B07GDL1TSN/ref=sr_1_3?dchild=1&keywords=Higo+Mini+A+cable+bafang&qid=1593279954&sr=8-3)

3. `An XL6009 DC-DC Voltage Step Up Boost Converter` to take a 5V supply from your laptop and then boost it to the 30v required to drive the 860C LCD while it is being updated.

![xl6009](images/2020/06/xl6009.png)

[Ebay search](https://www.ebay.co.uk/sch/i.html?_from=R40&_trksid=p2334524.m570.l1313.TR2.TRC1.A0.H0.XXL6009.TRS0&_nkw=XL6009&_sacat=0&LH_TitleDesc=0&_osacat=0&_odkw=Higo+Mini+A+cable+5+pin)



When assembled, the `bootloader` looked liked this for me

![bootloader assembly](images/2020/06/bootloader-assembly.png)

Now that we have built the `bootloader`, we need to adjust the voltage supply that will reach the 860c display LCD.

## Adjusting the output voltage from the DC Booster

Check that the jumpers on your `CH340G` are set to provide `5 volts` and not `3.3 volts` as below.

![5 volts](images/2020/06/5-volts.png)

You will see that the USB connection from your laptop will supply 5 volts to the `in+` `in-` side of the `XL6009 DC Step up boost converter`.

Check the voltage delivered to the `XL6009` ....

![checking input voltage](images/2020/06/checking-input-voltage.png)

We now need to adjust the `XL6009` so that we are delivering the required voltage to the `860c` LCD display.

You need to adjust the potentiometer (little screw on the blue block) so that the output voltage from the buck converter is 30 volts. You will need to use your multimeter to measure the DC voltage on the `+out` and `-out` side of the `XL6009`.

![adjusting output voltage](images/2020/06/adjusting-output-voltage.png)

Now we have 30 volts output and are ready to flash the `860c` LCD display.

![we have 30v](images/2020/06/we-have-30v.png)
