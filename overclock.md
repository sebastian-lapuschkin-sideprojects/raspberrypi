Overclocking the pi is actually quite easy.
Just follow the few lines to execute described [in the magpi magazine](https://magpi.raspberrypi.org/articles/how-to-overclock-raspberry-pi-4).

I have set my pi to
```
arm_freq=1800
over_voltage=2
```

You can monitor your core temperature and clock speed with `watch vcgencmd measure_clock arm ; sensors`.
After half an hour of "Sending mit der Maus" full hd video playback via browser,
which is probably the longest sequence under constant load of my setup,
my passively cooled and suboptimally placed RasPi4 never exceeded 67.2°C.
Everything below 80° is ok, and the instances of micro-stutters the
video freezing due to the processor hitting 100% load are eliminated. 
