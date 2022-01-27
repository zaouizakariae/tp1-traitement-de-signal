# ANALYSE SPECTRAL D’UN SIGNAL

## Introduction :

Le concept le plus important dans l'analyse du domaine fréquentiel est la transformation. La transformation est utilisée pour convertir une fonction de domaine temporel en une fonction de domaine fréquentiel et inversement. La transformation la plus courante utilisée dans le domaine fréquentiel est la transformation de Fourier. La transformation de Fourier est utilisée pour convertir un signal de n'importe quelle forme en une somme d'un nombre infini d'ondes sinusoïdales. L'analyse des fonctions sinusoïdales étant plus facile que l'analyse des fonctions de forme générale, cette méthode est très utile et largement utilisée. Dans ce Tp nous allons exploite la transformée de Fourier discrète qui est un outil mathématique de traitement du signal numérique, qui est l'équivalent discret de la transformée de Fourier continue qui est utilisée pour le traitement du signal analogique

## Représentation temporelle et fréquentielle:

Considérons un signal périodique x(t) constitué d’une somme de deux sinusoïdes de fréquences 15Hz et 20Hz :
   - 𝐱(𝐭) = 𝐬𝐢𝐧(𝟐𝝅𝟏𝟓𝒕) + 𝐬𝐢𝐧(𝟐𝝅𝟐𝟎𝒕)
- On trace le signal x(t) dans un intervalle de temps : 0, 10-Te. Avec Te=1/50 Ensuite ,pour générer le son du signal on a appliqué la fonction sound(x,1000)

x :la fonction et 1000 la fréquence avec laquelle on veut entendre le son. Après pour le visualiser on le trace dans une figure a l’aide de la commande plot(t,x)

le script descriptif :

```matlab
Te=1/50;
t=0:Te:10-Te;
x=sin(2*pi*15*t)+sin(2*pi*20*t);
sound(x,1000)
subplot(3,2,1)
plot(t,x)
```
- Pour bien visualiser le signal on doit passer au domaine fréquentiel en appliquant la commande fft(x) qui calcule la transformée de Fourier : une méthode qui permet de décrire un signal discret en fonction de la fréquence. Ensuite fftshift(x) qui réorganise une transformée de Fourier X en déplaçant la composante de fréquence nulle vers le centre du réseau. On les trace à travers la commande plot

le script descriptif :

```matlab
f=(0:500-1)*(50/500)
y=fft(x);
subplot(3,2,2)
plot(f,abs(y));
t1=(-500/2:(500/2)-1)*(50/500);
z=fftshift(abs(y));
subplot(3,2,3)
plot(t1,z)
```

- On a introduit un bruit blanc gaussien noise la commande randn qui renvoie un scalaire aléatoire tiré de la distribution normale standard dans le signal d’origine x(t) pour créer un nouveau signal xnoise ,ensuite on utilise fft pour savoir les fréquences qui constituent le nouveau signal. Pour le visualiser on le trace avec la commande plot. Enfin ,on applique qui réorganise les sorties de fft en déplaçant la composante de fréquence nulle au centre du tableau. Il est utile pour visualiser une transformée de Fourier avec la composante de fréquence nulle au milieu du spectre.

le script descriptif :
 
```matlab
noise=2*randn(size(t))
xnoise=x+noise
sound(xnoise,1000)
subplot(3,2,4)
plot(t,xnoise)
p=fft(xnoise);
subplot(3,2,5)
plot(f,abs(p))
k=fftshift(abs(p));
subplot(3,2,6)
plot(t1,k)
```

La visualisation des fonctions est faite sur le meme plot divisé en utilisant la commande subplot et on a obtenu la figure suivante :

![xnoise](https://user-images.githubusercontent.com/85891554/151396195-3e13e46f-82c9-4731-88b7-16aa115b6e0d.jpg)

## Analyse fréquentielle du chant du rorqual bleu

Le but de cet exercice est d’extraire le chant du rorqual bleu du fichier ‘bluewhale.au’ .Ce chant se trouve entre les deux fréquences x=2.45e4 z=3.1e4 après on l entend a travers la commande sound et finalement on le trace avec la commande plot dans un intervalle de temps 

```matlab
t=15*(0:1/Fs:(length(rorqualvoice)-1)*(1/Fs)) 
```

le script descriptif :

```matlab
filename ='tutorials_resource_files_bluewhale.au';
[y,Fs]= audioread(filename)
rorqualvoice=y(x:z);
t=15*(0:1/Fs:(length(rorqualvoice)-1)*(1/Fs));
sound(rorqualvoice,Fs)
figure(1)
plot(t,rorqualvoice)
```

![Capture d’écran 2022-01-27 170444](https://user-images.githubusercontent.com/85891554/151396741-57f268fc-68bc-4de7-b766-4812f480483e.png)

Pour identifier les composantes fréquentielles de ce signal audio ,on applique la transformée de Fourrier

```matlab
j=abs(fft(rorqualvoice)).^2/length(rorqualvoice);
f=[-length(rorqualvoice)/2:length(rorqualvoice)/2-1]*(Fs/length(rorqualvoice))/10;
plot(f,fftshift(j))
```

![Capture_decran_816](https://user-images.githubusercontent.com/85891554/151397060-45fda191-b085-449f-a5b4-b998a795d11d.png)

Spectre billateral ou on peut visualiser les differentes frequences qui constituent le signal du chant du rorqual bleu

## Conclusion

Dans ce Tp ,nous avons pu découvrir la représentation de signaux et les applications de la transformée de Fourier discrète (TFD) sous Matlab. Ainsi que , l’évaluation de l’intérêt du passage du domaine temporel au domaine fréquentiel dans l’analyse et l’interprétation des signaux physiques réels.
