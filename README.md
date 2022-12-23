# FDV_08_Cinemachine

FDV_08_Cinemachine

1. Reutilizamos el zombi y el duende de los ejercicios anteriores y luego agregamos una cámara Cinemachine 2D.
En la propiedad **Follow**, hacemos referencia a nuestro zombi y dejamos la propiedad Mirar como ninguno y en la propiedad **body > Tracked Object Offset** del objeto rastreado, cambiamos X a un valor mayor que 0, lo que hace que la cámara se enfoque en una posición frente al zombi.  No cambiamos la prioridad de la cámara, que está en 10.

    ![Controlador de cámara -ejercicio 1](https://github.com/almadacv/FDV_08_Cinemachine/blob/main/Gif/VCam1.png)

    ![Controlador de cámara -ejercicio 1](https://github.com/almadacv/FDV_08_Cinemachine/blob/main/Gif/VCam1.gif)

2. Duplicamos el goblin, y le agregamos una cámara Cinemachine del **tipo Target Group Camera** y en la propiedad le agregamos los goblins al _TargetGroup_, dependiendo del valor del _peso_ y el _radio_ que le agregamos a los goblins, tenemos la cámara a pesar del movimiento de los goblins centrándolos en la pantalla.

    ![Controlador de cámara -ejercicio 2](https://github.com/almadacv/FDV_08_Cinemachine/blob/main/Gif/VCam2.png)

    ![Controlador de cámara -ejercicio 2](https://github.com/almadacv/FDV_08_Cinemachine/blob/main/Gif/VCam2.gif)

3. Para completar, crearemos un **Gameobject vacío** y agregaremos un Colisionador de tipo **Polygyne** y activaremos la propiedad _Is Trigger_ y __añadimos__ la extensión _CinemachineConfiner_ a la cámara y en _BoundingShape2D_ referenciamos nuestro gameobject y activamos la opción *Confine Screen Edge*.

    ![Controlador de cámara -ejercicio 3](https://github.com/almadacv/FDV_08_Cinemachine/blob/main/Gif/VCam3.gif)

4. Repetimos el ejercicio anterior, solo reduciendo el área del colisionador de GameObject. La diferencia que se observa es que cuando la cámara choca con el límite del gameObject, dejará de seguir al personaje si sale del área delimitada por el colisionador.

    ![Controlador de cámara -ejercicio 4](https://github.com/almadacv/FDV_08_Cinemachine/blob/main/Gif/VCam4.gif)

5. En este ejercicio, agregaremos un componente **Cinemachine Collision Impulse Source**  al goblin y agregaremos un **Cinemachine Impulse Listener** a nuestra cámara.

    ![Controlador de cámara -ejercicio 5](https://github.com/almadacv/FDV_08_Cinemachine/blob/main/Gif/VCam5.gif)

6. Repetimos los pasos desde el punto 1 y agregamos una nueva cámara 2D, hacemos referencia al duende en la propiedad **Follow**.

    ![Controlador de cámara -ejercicio 6](https://github.com/almadacv/FDV_08_Cinemachine/blob/main/Gif/VCam6.gif)

7. Para obtener el resultado deseado, creamos dos variables del tipo GameObject public donde hacemos referencia a las cámaras respectivas, y cuando queremos cambiar de cámara para _Habilitar/Deshabilitar_ el GameObject.

    ```C#
    public GameObject CVirt;
    public GameObject CVirt2;

    if (Input.GetKeyDown(KeyCode.T) && CVirt)
        {
            CVirt.SetActive(true);
            CVirt2.SetActive(false);
        }
        else if (Input.GetKeyDown(KeyCode.Y) && CVirt)
        {
            CVirt.SetActive(false);
            CVirt2.SetActive(true);
        }
    ```

    ![Controlador de cámara -ejercicio 7](https://github.com/almadacv/FDV_08_Cinemachine/blob/main/Gif/VCam7.gif)

8. Cambiamos el atributo Ruido de nuestra cámara virtual de Ninguno a BasicMultiChannelPerlin, podemos cambiar los valores de amplitud y frecuencia, pero ¿cómo los cambio vía script?, solo cambio la frecuencia a 20 para que podamos visualizar mejor el resultado.
luego agregamos variables públicas del tipo CinemachineVirtualCamera y NoiseSettings.
en el inspector, para NoiseSetting hacemos referencia al ruido Handheld_normal_extreme, al que se puede hacer referencia cualquiera y para CinemachineVirtualCamera hacemos referencia a nuestra cámara.

        ```C#

        public CinemachineVirtualCamera VirtCam;
        public CinemachineBasicMultiChannelPerlin CmMultChan;
        public NoiseSettings CmNoiseProfile;
        private float NoiseAmpCam = 10.0f;

        void Start()
        {
            CmMultChan = VirtCam.GetCinemachineComponent<CinemachineBasicMultiChannelPerlin>();
        }

         if (Input.GetKeyDown(KeyCode.F) && CmMultChan)
            {
                CmMultChan.m_NoiseProfile = CmNoiseProfile;
                CmMultChan.m_FrequencyGain = NoiseAmpCam;
                CmMultChan.m_AmplitudeGain = (NoiseAmpCam - 40.0f);

                NoiseAmpCam = NoiseAmpCam + 50.0f;
            }
            else
            {
                CmMultChan.m_NoiseProfile = null;
            }
        ```

        Tendo isto no script ao verificamos se foi pulsada a tecla F e caso for atribuimos o noise Handheld_normal_extreme a propriedade m_NoiseProfile da nossa camara virtual e alteramos o valor da prorpriedade m_FrequencyGain (Frequencia) e m_AmplitudeGain (Amplitude) da mesma.

![Controlador de cámara -ejercicio Extra](https://github.com/almadacv/FDV_08_Cinemachine/blob/main/Gif/VCamExtra.gif)
