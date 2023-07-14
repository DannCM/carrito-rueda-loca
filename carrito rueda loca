#Tiene correcciones en dereha e izquierda.
import time
import network
import socket
from time import sleep
import machine
from machine import Pin

# RED WiFi
ssid = 'nombre de su red'
password = 'constraseña de su red'

# Asignación de Pins!
MotorA_Adelante = Pin(5, Pin.OUT)
MotorA_Atras = Pin(4, Pin.OUT)
MotorB_Adelante = Pin(3, Pin.OUT)
MotorB_Atras = Pin(2, Pin.OUT)

enA = Pin(6, Pin.OUT)
enB = Pin(7, Pin.OUT)


def adelante(duration):
    print('adelante')
    start_time = time.time()
    while time.time() - start_time < duration:
        enA.value(1)
        enB.value(1)
        MotorA_Adelante.value(0)
        MotorB_Adelante.value(0)
        MotorA_Atras.value(1)
        MotorB_Atras.value(1)


def reversa():
    enA(1)
    enB(1)

    MotorA_Adelante.value(1)
    MotorB_Adelante.value(1)
    MotorA_Atras.value(0)
    MotorB_Atras.value(0)
    print('reversa')


def stop():
    enA(1)
    enB(1)

    MotorA_Adelante.value(0)
    MotorB_Adelante.value(0)
    MotorA_Atras.value(0)
    MotorB_Atras.value(0)
    print('parar')


def izquierda():  # rueda izquierda detenida
    enA(0)
    enB(1)

    MotorA_Adelante.value(0)
    MotorB_Adelante.value(1)
    MotorA_Atras.value(0)
    MotorB_Atras.value(0)
    print('izquierda')


def derecha(duration):  # rueda derecha detenida
    start_time = time.time()
    while time.time() - start_time < duration:
        enA(1)
        enB(0)
        MotorA_Adelante.value(1)
        MotorB_Adelante.value(0)
        MotorA_Atras.value(0)
        MotorB_Atras.value(0)
    print('derecha')


def giroderecha(duration):
    print ('giraderecha')
    start_time = time.time()
    while time.time() - start_time < duration:
        
        #una rueda adelante, la otra atras
        enA(1)
        enB(1)
        MotorA_Adelante.value(1)
        MotorB_Adelante.value(0)
        MotorA_Atras.value(0)
        MotorB_Atras.value(1)


def giroizquierda():  # una rueda adelante, la otra atras
    enA(1)
    enB(1)

    MotorA_Adelante.value(0)
    MotorB_Adelante.value(1)
    MotorA_Atras.value(1)
    MotorB_Atras.value(0)
    print('gira izquierda')


# Detener el carrito
stop()


def trayectoriaCuadro():
    print('vector')
    adelante(0.2)
    stop()
    derecha(0.001)
    stop()
    adelante(0.2)
    stop()
    derecha(0.001)
    stop()
    adelante(0.2)
    stop()
    derecha(0.001)
    stop()
    adelante(0.2)
    stop()
    derecha(0.001)
    stop()
    stop()


def trayectoriaCircular():

    print('En circulos')
    for _ in range(6):
        adelante(0.0000001)
        stop()
        derecha(0.0000001)
        stop()
        adelante(0.0000001)
        stop()
        derecha(0.0000001)
        stop()


def connect():
    # Connect to WLAN
    wlan = network.WLAN(network.STA_IF)
    wlan.active(True)
    wlan.connect(ssid, password)
    while wlan.isconnected() == False:
        print('Esperando Conexión...')
        sleep(1)
    ip = wlan.ifconfig()[0]
    print(f'Conectado a {ip}')
    return ip


def open_socket(ip):
    # Open socket
    address = (ip, 80)
    connection = socket.socket()
    connection.bind(address)
    connection.listen(1)
    return connection


def webpage():
    # Template HTML
    html = f"""

    <!DOCTYPE html>
<html lang="es">

<head>
    <title>CARRITO RUEDA LOCA</title>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="AUTOR:" content="DANNA CRUZ">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

</head>

<header id="headr" style="width: 100%; height: 40px; position: static; background: pink; font-family:'century gothic'; padding: 10px 10px 50px 0; ">
        <section id="TOP">
            <div id="titulo">
                <ul>
                    <li>
                        <h1 style="text-align: center; color: #FF00DD; font-size:1.5em">CONTROL RUEDA LOCA</h1>
                    </li>
                </ul>
            </div>
        </section>
</header>

<body style="margin: 0; padding: 0; background-color: pink;">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/socket.io/4.5.4/socket.io.js"></script> <!-- include socket.io client side script -->
    <script> var socket = io(); //load socket.io-client and connect to the host that serves the page </script>

    <!--Inicio Controles-->
    <section id="controles" style="width: 100%; height: 400px;
        background: url(https://w0.peakpx.com/wallpaper/30/833/HD-wallpaper-artistic-mountain-pink-minimalist.jpg) 50% 0 ; background-size: cover; background-position:center;">
    <div id="control" style="position: relative; top: 25px; width: 60%; height: 90%; margin: 0 auto; background-color: rgba( 245, 176, 208, 0.5); border-radius: 50px;">  
        </td>

        <center>
            <form action="./adelante">              
                <input type="submit" value="FORWARD " 
                style="background-color: #FF0077;
                border-radius: 05px; width:80px; height:45px;"/> 
            </form>

            <table >
                <tr>
                    <td>
                        <form action="./giroizquierda">
                        <input type="submit" value="TURN LEFT" 
                        style="background-color: #FF0077;
                        border-radius: 05px; width:95px; height:45px;"/> 
                        </form>
                    </td>
                    <td>
                        <form action="./izquierda">
                        <input type="submit" value="LEFT" 
                        style="background-color: #FF0077;
                        border-radius: 05px; width:65px; height:45px;"/> 
                        </form>
                    </td>

                    <td>
                        <form action="./stop">
                        <input type="submit" value="STOP" 
                        style="background-color: #FF0077;
                        border-radius: 05px; width:65px; height:45px;"/> 
                        </form>
                    </td>
                    <td>
                        <form action="./derecha">
                        <input type="submit" value="RIGTH" 
                        style="background-color: #FF0077;
                        border-radius: 05px; width:65px; height:45px;"/>
                        </form>
                    </td>
                    <td>
                        <form action="./giroderecha">
                        <input type="submit" value="TURN RIGTH" 
                        style="background-color: #FF0077;
                        border-radius: 05px; width:95px; height:45px;"/>
                        </form>
                    </td>
                    <td>
                        <form action="./trayectoriaCuadro">
                        <input type="submit" value="VECTOR" 
                        style="background-color: #FF0077;
                        border-radius: 05px; width:65px; height:45px;"/>
                        </form>
                    </td>
                </tr>
            </table>

            <form action="./reversa">
                        <input type="submit" value="REVERSE" 
                        style="background-color: #FF0077;
                        border-radius: 05px; width:80px; height:45px;"/>

            <form action="./trayectoriaCircular">
                        <input type="submit" value="ARROUND" 
                        style="background-color: #FF0077;
                        border-radius: 05px; width:80px; height:45px;"/>


                </table>
        </center>
    </div>
    </section><!--controles-->
</body>

</html>
            """
    return str(html)


def serve(connection):
    # Inicio del servidor
    while True:
        client = connection.accept()[0]
        request = client.recv(1024)
        request = str(request)
        try:
            request = request.split()[1]
        except IndexError:
            pass
        if request == '/adelante?':
            adelante(2)
        elif request == '/izquierda?':
            izquierda()
        elif request == '/stop?':
            stop()
        elif request == '/derecha?':
            derecha(2)
        elif request == '/reversa?':
            reversa()
        elif request == '/giroderecha?':
            giroderecha(2)
        elif request == '/giroizquierda?':
            giroizquierda()
        elif request == '/trayectoriaCuadro?':
            trayectoriaCuadro()
        elif request == '/trayectoriaCircular?':
            trayectoriaCircular()

        html = webpage()
        client.send(html)
        client.close()


try:
    ip = connect()
    connection = open_socket(ip)
    serve(connection)
except KeyboardInterrupt:
    machine.reset()
