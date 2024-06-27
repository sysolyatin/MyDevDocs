# Затухание анимации в AE

Можно применить, например, для скейла. На нужном (последнем) ключевом кадре нажать с альтом зажать иконку таймера 
и в открывшееся поле ввести код:

```C
n = 0;
if (numKeys > 0){
	n = nearestKey(time).index;
	if (key(n).time > time) {
		n--;
	}
}
if (n == 0) {
	t = 0;
}
else {
	t = time - key(n).time;
}
 
if (n > 0) {
	v = velocityAtTime(key(n).time - thisComp.frameDuration/10);
	amp = .025;
	freq = 2.0;
	decay = 3.0;
	value + v*amp*Math.sin(freq*t*2*Math.PI)/Math.exp(decay*t);
}
else {
	value;
}
```