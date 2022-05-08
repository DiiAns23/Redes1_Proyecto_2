<div id="indice">

-----------------------------------------
## **INDICE** 📚
-----------------------------------------

-   [*Indice*](#indice)
-   [*Integrantes*](#integrantes)
-   [*Como subdividir una Red*](#topo)
-   [*Red Topología 1*](#cls)
    - [*Calcular el número de bits de subred necesarios*](#cl1)
    - [*Obtener las subredes*](#cl2)
    - [*Calcular los parámetros de cada subred*](#cl3)
    - [*Configuracion de Red*](#cl4)
    - [*Resultado*](#result)
-   [*Red Topología 2*](#cls2)
    - [*Calcular el número de bits de subred necesarios*](#cl5)
    - [*Obtener las subredes*](#cl6)
    - [*Calcular los parámetros de cada subred*](#cl7)
    - [*Configuracion de Red*](#cl8)
    - [*Resultado*](#result2)
-   [*Red Topología 3*](#cls3)
    - [*Calcular el número de bits de subred necesarios*](#cl9)
    - [*Obtener las subredes*](#cl10)
    - [*Calcular los parámetros de cada subred*](#cl11)
    - [*Configuracion de Red*](#cl12)
    - [*Resultado*](#result3)

<div id = "integrantes">

## Integrantes
| Nombre | Carne | 
|--------|-------|
| Diego Andrés Obín Rosales | 201903865 | 
| Juan Diego Alvarado Salguero | 201807335 |
| Erick Jose Andre Villatoro Revolorio | 201900907 |
| Josué David Zea Herrera| 201807159 | 
| Deivid Alexander Lux Revolorio | 201549059 |



<div id = "topo">

## **COMO SUBDIVIDIR UNA RED**

_FLSM del Inglés **Fixed Length Subnet Mask** o **Máscara de Subred de Longitud Fariable** es la forma tradicional de subdividir una red, consiste en "tomar prestados" unos bits en la parte de host para generar nuevas subredes._

Entonces, para este caso de ejemplo vamos a subdividir la red 10.4.0.0 /16 para subdividirla en 16384 subreedes.

<div id="cls">

## **RED TOPOLOGIA 1 📋**

<div id="cl1">

## *Calcular el número de bits de subred necesarios*
- Ya que nuestra dirección ip tiene el prefijo /16 esto significa que 16 bits representan la parte de red y 16 bits la parte de host. Se puede visualizar de la siguiente forma:

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/1.png">
    </p>
</div>

- Para determinar el número de bits que hay que tomar de la parte de host para obtener 16384 subredes se utiliza la expresión:
```
2² ≥ 16384
```

Donde **n** es el número de bits necesarios. Para obtener **n** se puede utilizar la tabla siguiente:

| Valor de n | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
| ------ | -- | -- | -- | -- | -- | --  | -- | -- |
| N° subredes |  1 | 2 | 4 | 8 | 16 | 32 | 64 | 128 |

Esta tabla se puede prolongar todo lo que se quiera calculando potencias de 2. En nuestro caso

```
2¹⁴ = 16384 ≥ 16384 ⇒ n = 14
```

Por lo que hay que tomar **14 bits** en la parte del host como se muestra:

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/2.png">
    </p>
</div>

Esto significa que las subredes tendrán el prefijo /30. Convirtiendo a decimal cada uno de los octetos se obtiene la nueva máscara de subred, que será la misma para todas las subredes, de ahí se obtiene el prefijo _Máscara fija._
```
255.255.255.252
```
<div id="cl2">

## *Obtener las subredes*
- Para obtener la dirección de red de cada subred basta con cambiar los bits de subred calculados en el paso anterior. En nuestro caso hay **16384** posibles combinaciones desde 00000000000000 hasta 11111111111111 cada una de las combinaciones es una dirección de red diferente. Esto se aplica de la siguiente forma :
<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/3.png">
    </p>
</div>

_**NOTA:** Si no se siente cómodo con los números, también puede obtener las direcciones de red a travéz del llamado **salto de red** que es la diferencia entre dos direcciones de red consecutivas. El salto de red se calcula como la diferencia entre **256** y el valor del **último octeto no nulo** de la misma máscara. En este caso sería_
```
S = 256 - 252 = 4
```

Entonces para obtener las direcciones de red solo tiene que ir sumando a la dirección de red original el valor del respectivo salto.
<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/4.png">
    </p>
</div>

<div id="cl3">

## *Calcular los parámetros de cada subred*

El número de host por subred se calcula de la siguiente forma:
```
H = 2ⁿ - 2
```

En este caso **n** es el número de bits de la parte de host (bits azules en los pasos anteriores). El -2 de la fórmula se debe a que la primera dirección corresponde a la dirección de red y la última corresponde a la dirección de broadcast, por lo que no se las puede asignar a ningún host. Teniendo esto en cuenta, el número de hosts por cada una de nuestras subredes es
```
H = 2² - 2 = 2
```

Para calcular el resto de parámetros tomaremos como referencia la primera subred ya que el proceso es el mismo para el resto de subredes.

Las direcciones de host se obtienen combinando los bits de host desde **01** hasta **10**. De esta forma obtenemos las del **primero y el último host**
```
10.4.00000000.00000001 ⇒ 10.4.0.1 
10.4.00000000.00000010 ⇒ 10.4.0.2
```

La dirección de **broadcast** se obtiene haciendo 1 todos los bits de la parte del host
```
10.4.00000000.00000011 ⇒ 10.4.0.3
```

_**NOTA:** Si lo desea puede realizar los calculos sin utilizar números binaios de la manera siguiente_

1. La dirección del primer host se obtiene **sumando 1 a la dirección de red.**
```
10.4.0+10 ⇒ 10.4.0.1
```

2. La dirección del último host se obtiene **sumando a la dirección de red el número de hosts por subred.**
```
10.4.0+20 ⇒ 10.4.0.2
```

2. La dirección de broadcast se obtiene **Sumando 1 a la dirección del último host**

```
10.4.2+10 ⇒ 10.4.0.3
```

<div id="cl4">

## **CONFIGURACION DE RED**

## *R2*
```shell
configure terminal
int s3/1
ip address 10.4.0.5 255.255.255.252
no shutdown
exit

int f0/0
ip address 10.4.0.13 255.255.255.252
no shutdown
exit

ip route 192.168.44.0 255.255.255.0 10.4.0.6
ip route 10.4.0.20 255.255.255.252 10.4.0.14
ip route 192.168.45.0 255.255.255.0 10.4.0.14

end

copy running-config startup-config

```


## *R3*
```shell
configure terminal
int s3/0
ip address 10.4.0.1 255.255.255.252
no shutdown
exit

int f0/0
ip address 10.4.0.9 255.255.255.252
no shutdown
exit


ip route 192.168.44.0 255.255.255.0 10.4.0.2
ip route 10.4.0.16 255.255.255.252 10.4.0.10
ip route 192.168.45.0 255.255.255.0 10.4.0.10
exit


copy running-config startup-config

```

## *R4*
```shell
configure terminal
int s3/1
ip address 10.4.0.17 255.255.255.252
no shutdown
exit

int f0/0
ip address 10.4.0.10 255.255.255.252
no shutdown
exit

ip route 192.168.45.0 255.255.255.0 10.4.0.18
ip route 10.4.0.0 255.255.255.252 10.4.0.9
ip route 192.168.44.0 255.255.255.0 10.4.0.9

exit


copy running-config startup-config

```

## *R5*
```shell
configure terminal
int s3/0
ip address 10.4.0.21 255.255.255.252
no shutdown
exit

int f0/0
ip address 10.4.0.14 255.255.255.252
no shutdown
exit

ip route 192.168.45.0 255.255.255.0 10.4.0.22
ip route 10.4.0.4 255.255.255.252 10.4.0.13
ip route 192.168.44.0 255.255.255.0 10.4.0.13

exit

copy running-config startup-config

```

<div id="result">

## **RESULTADOS**

![Tabla de resultados](https://github.com/Josue-Zea/pruebas/blob/master/pictures/Tabla.png "This is a sample image.")

Si desea probar la calculadora FLSM puede hacerlo dando click [aqui](https://arcadio.gq/calculadora-subredes-flsm.html).



<div id="cls2">

### **RED TOPOLOGIA 2 📋**

<div id="cl5">

## *Calcular el número de bits de subred necesarios*
- Nuestra dirección ip tiene el prefijo /24, esto siginifica que 24 bits representan la parte de red y 8 bits a la parte de host, esto se representa de la forma:

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/21.png">
    </p>
</div>

- Para determinar el número de bits que hay que tomar de la parte de host para obtener 4 subredes se utiliza la expresión:
```
2² ≥ 4
```

Donde **n** es el número de bits necesarios. Para obtener **n** se puede utilizar la tabla siguiente:

| Valor de n | 0 | 1 | **2** | 3 | 4 | 5 | 6 | 7 |
| ------ | -- | -- | -- | -- | -- | --  | -- | -- |
| N° subredes |  1 | 2 | **4** | 8 | 16 | 32 | 64 | 128 |

Esta tabla se puede prolongar todo lo que se quiera calculando potencias de 2. En nuestro caso

```
2² = 4 ≥ 4 ⇒ n = 2
```

Por lo que hay que tomar **2 bits** en la parte del host como se muestra:

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/22.png">
    </p>
</div>

Esto significa que las subredes tendrán el prefijo /26. Convirtiendo a decimal cada uno de los octetos se obtiene la nueva máscara de subred, que será la misma para todas las subredes, de ahí se obtiene el prefijo _Máscara fija._
```
255.255.255.192
```

<div id="cl6">

## *Obtener las subredes*
- Para obtener la dirección de red de cada subred basta con cambiar los bits de subred calculados en el paso anterior. En nuestro caso hay **4** posibles combinaciones desde **_00_** hasta **_11_** cada una de las combinaciones es una dirección de red diferente. Esto se aplica de la siguiente forma :

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/23.png">
    </p>
</div>

_**NOTA:** Si no se siente cómodo con los números, también puede obtener las direcciones de red a travéz del llamado **salto de red** que es la diferencia entre dos direcciones de red consecutivas. El salto de red se calcula como la diferencia entre **256** y el valor del **último octeto no nulo** de la misma máscara. En este caso sería_
```
S = 256 - 192 = 64
```

Entonces para obtener las direcciones de red solo tiene que ir sumando a la dirección de red original el valor del respectivo salto.
<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/24.png">
    </p>
</div>

<div id="cl7">

## *Calcular los parámetros de cada subred*

El número de host por subred se calcula de la siguiente forma:
```
H = 2ⁿ - 2
```

En este caso **n** es el número de bits de la parte de host (bits azules en los pasos anteriores). El -2 de la fórmula se debe a que la primera dirección corresponde a la dirección de red y la última corresponde a la dirección de broadcast, por lo que no se las puede asignar a ningún host. Teniendo esto en cuenta, el número de hosts por cada una de nuestras subredes es
```
H = 2⁶ - 2 = 2
```

Para calcular el resto de parámetros tomaremos como referencia la primera subred ya que el proceso es el mismo para el resto de subredes.

Las direcciones de host se obtienen combinando los bits de host desde **000001** hasta **111110**. De esta forma obtenemos las del **primero y el último host**

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/25.png">
    </p>
</div>

La dirección de **broadcast** se obtiene haciendo 1 todos los bits de la parte del host

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/26.png">
    </p>
</div>

_**NOTA:** Si lo desea puede realizar los calculos sin utilizar números binaios de la manera siguiente_

1. La dirección del primer host se obtiene **sumando 1 a la dirección de red.**

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/27.png">
    </p>
</div>

2. La dirección del último host se obtiene **sumando a la dirección de red el número de hosts por subred.**

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/28.png">
    </p>
</div>

2. La dirección de broadcast se obtiene **Sumando 1 a la dirección del último host**

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/29.png">
    </p>
</div>


<div id="cl8">

## **CONFIGURACION DE RED**

<div id="cls3">

### **RED TOPOLOGIA 3 📋**

<div id="cl9">

## *Calcular el número de bits de subred necesarios*
- Nuestra dirección ip tiene el prefijo /24, esto siginifica que 24 bits representan la parte de red y 8 bits a la parte de host, esto se representa de la forma:

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/21.png">
    </p>
</div>

- Para determinar el número de bits que hay que tomar de la parte de host para obtener 4 subredes se utiliza la expresión:
```
2² ≥ 4
```

Donde **n** es el número de bits necesarios. Para obtener **n** se puede utilizar la tabla siguiente:

| Valor de n | 0 | 1 | **2** | 3 | 4 | 5 | 6 | 7 |
| ------ | -- | -- | -- | -- | -- | --  | -- | -- |
| N° subredes |  1 | 2 | **4** | 8 | 16 | 32 | 64 | 128 |

Esta tabla se puede prolongar todo lo que se quiera calculando potencias de 2. En nuestro caso

```
2² = 4 ≥ 4 ⇒ n = 2
```

Por lo que hay que tomar **2 bits** en la parte del host como se muestra:

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/22.png">
    </p>
</div>

Esto significa que las subredes tendrán el prefijo /26. Convirtiendo a decimal cada uno de los octetos se obtiene la nueva máscara de subred, que será la misma para todas las subredes, de ahí se obtiene el prefijo _Máscara fija._
```
255.255.255.192
```

<div id="cl10">

## *Obtener las subredes*
- Para obtener la dirección de red de cada subred basta con cambiar los bits de subred calculados en el paso anterior. En nuestro caso hay **4** posibles combinaciones desde **_00_** hasta **_11_** cada una de las combinaciones es una dirección de red diferente. Esto se aplica de la siguiente forma :

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/23.png">
    </p>
</div>

_**NOTA:** Si no se siente cómodo con los números, también puede obtener las direcciones de red a travéz del llamado **salto de red** que es la diferencia entre dos direcciones de red consecutivas. El salto de red se calcula como la diferencia entre **256** y el valor del **último octeto no nulo** de la misma máscara. En este caso sería_
```
S = 256 - 192 = 64
```

Entonces para obtener las direcciones de red solo tiene que ir sumando a la dirección de red original el valor del respectivo salto.
<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/24.png">
    </p>
</div>

<div id="cl11">

## *Calcular los parámetros de cada subred*

El número de host por subred se calcula de la siguiente forma:
```
H = 2ⁿ - 2
```

En este caso **n** es el número de bits de la parte de host (bits azules en los pasos anteriores). El -2 de la fórmula se debe a que la primera dirección corresponde a la dirección de red y la última corresponde a la dirección de broadcast, por lo que no se las puede asignar a ningún host. Teniendo esto en cuenta, el número de hosts por cada una de nuestras subredes es
```
H = 2⁶ - 2 = 2
```

Para calcular el resto de parámetros tomaremos como referencia la primera subred ya que el proceso es el mismo para el resto de subredes.

Las direcciones de host se obtienen combinando los bits de host desde **000001** hasta **111110**. De esta forma obtenemos las del **primero y el último host**

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/25.png">
    </p>
</div>

La dirección de **broadcast** se obtiene haciendo 1 todos los bits de la parte del host

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/26.png">
    </p>
</div>

_**NOTA:** Si lo desea puede realizar los calculos sin utilizar números binaios de la manera siguiente_

1. La dirección del primer host se obtiene **sumando 1 a la dirección de red.**

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/27.png">
    </p>
</div>

2. La dirección del último host se obtiene **sumando a la dirección de red el número de hosts por subred.**

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/28.png">
    </p>
</div>

2. La dirección de broadcast se obtiene **Sumando 1 a la dirección del último host**

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/29.png">
    </p>
</div>


<div id="cl12">

## **CONFIGURACION DE RED**
## *SW2*

- ### *CONFIGURACION DE VLAN'S*
```shell
configure terminal
vlan 10
name RHUMANOS
exit
vlan 20
name CONTABILIDAD
exit
vlan 30
name VENTAS
exit
vlan 40
name INFORMATICA
exit

spanning-tree vlan 10 root primary
spanning-tree vlan 20 root primary
spanning-tree vlan 30 root primary
spanning-tree vlan 40 root primary

do sh vlan-sw
```

- ### *CONFIGURACION DE PUERTOS*
  
```shell
hostname CD
vtp domain GRUPO4
vtp password grupo4
vtp version 2
vtp mode server
exit

sh vtp status
configure terminal
int f1/0
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

int f1/1
switchport mode access
switchport acces vlan 30
exit

int f1/2
switchport mode access
switchport acces vlan 20
exit

int f1/3
switchport mode access
switchport acces vlan 10
exit

int f1/4
switchport mode access
switchport acces vlan 40
exit

exit

copy running-config startup-config
```

## *R6*
```shell
conf t
int f0/0.10
exit
int f0/0.20
exit
int f0/0.30
exit
int f0/0.40
exit
do sh ip int br

int f0/0
no shutdown
exit

int f0/0.10
encapsulation dot1Q 10
ip address 192.168.45.62 255.255.255.192
no shutdown
exit

int f0/0.20
encapsulation dot1Q 20
ip address 192.168.45.126 255.255.255.192
no shutdown
exit

int f0/0.30
encapsulation dot1Q 30
ip address 192.168.45.190 255.255.255.192
no shutdown
exit

int f0/0.40
encapsulation dot1Q 40
ip address 192.168.45.254 255.255.255.192
no shutdown
exit

int s3/0
ip address 10.4.0.22 255.255.255.252
no shutdown
exit

int s3/1
ip address 10.4.0.18 255.255.255.252
no shutdown
exit

ip route 10.4.0.8 255.255.255.252 10.4.0.17
ip route 10.4.0.12 255.255.255.252 10.4.0.21

ip route 10.4.0.0 255.255.255.252 10.4.0.17
ip route 10.4.0.4 255.255.255.252 10.4.0.21

ip route 192.168.44.0 255.255.255.0 10.4.0.17
ip route 192.168.44.0 255.255.255.0 10.4.0.21

exit

sh ip int br

copy running-config startup-config

```

## *Asignacion de IP's a las VPC'S*

- ### Recursos Humanos
  ```shell
  ip 192.168.45.1 255.255.255.224 192.168.45.62
  ```
  
- ### Ventas
  ```shell
  ip 192.168.45.129 255.255.255.128 192.168.45.190
  ```

- ### Informatica
  ```shell
  ip 192.168.45.193 255.255.255.192 192.168.45.254
  ```

- ### Contabilidad
  ```shell
  ip 192.168.45.165 255.255.255.240 192.168.45.254
  ```
  
<div id="result3">

## **RESULTADOS**

![Tabla de resultados](https://github.com/Josue-Zea/pruebas/blob/master/pictures/Tabla.png "This is a sample image.")

Si desea probar la calculadora FLSM puede hacerlo dando click [aqui](https://arcadio.gq/calculadora-subredes-flsm.html).

<div id="result2">

## **RESULTADOS**

![Tabla de resultados](https://github.com/Josue-Zea/pruebas/blob/master/pictures/Tabla.png "This is a sample image.")

Si desea probar la calculadora FLSM puede hacerlo dando click [aqui](https://arcadio.gq/calculadora-subredes-flsm.html).

