# splane


## Descripcion

Herramientas para el diseño y análisis de filtros analógicos y digitales.
Se basa fuertemente en las funciones provistas por [`scipy.signal`](https://docs.scipy.org/doc/scipy/reference/signal.html)
y las extendiende.


## ¿Cómo instalar el paquete?

```
pip3 install splane
```

## ¿Cómo trabajar con los fuentes?

### Setup

1- Crear un entorno virtual (correr esto en la raíz del repositorio):

  ```sh
  python3 -m venv .
  source bin/activate
  ```

2- Instalar las depedencias:

  ```sh
   pip3 install -r requirements.txt
  ```

### Probar el codigo

1- Abrir una consola de python3 en `src`:

   ```sh
   cd src/
   python3
   ```

2- Importar `splane` y usar:

  ```python
  from tc2 import splane
  from scipy.signal import TransferFunction, buttap, zpk2tf

  z,p,k = buttap(3) # Creo un filtro Butterworth de orden 3
  num, den = zpk2tf(z, p, k) # Obtengo el numerador y denominador.
  tf = TransferFunction(num, den) # Obtengo la funcion transferencia.
  
  # Grafico algunas partes de funcion (modulo, fase, retardo
  splane.bodePlot(tf)
  splane.GroupDelay(tf)
  # Grafico las raices y los ceros.
  splane.pzmap(tf)
  ```

## ¿Cómo actualizar el paquete?

### Subir una nueva version

1- Testear el paquete.
2- Actualizar el CHANGELOG con los datos de la nueva release.
3- Actualizar la version en `setup.cfg`.
4- Correr lo siguiente para generar los archivos de distribución:

  ```sh
  python3 -m build
  ```

5- Correr lo siguiente para subir la nueva versión del paquete al [repositorio de prueba](https://test.pypi.org/) (pide usuario y contraseña):

  ```sh
  python3 -m twine upload --repository testpypi dist/*
  ```

### Testear la instalacion

1- Crear un nuevo entorno virtual (correr en otro directorio que no sea el repositorio mismo):

  ```sh
  mkdir test_splane_env
  cd test_splane_env
  python3 -m venv .
  source bin/activate
  ```

2- Instalar el paquete desde el repositorio de prueba:

  ```sh
  python3 -m pip install --index-url https://test.pypi.org/simple/ --no-deps splane-agalbachicar
  ```

3- Probar el importado y las dependencias. Tratar la misma prueba con el Butterworth del ejemplo anterior.

