# Protección de credenciales

**¿Qué ocurriría si una persona obtiene acceso de lectura a esta tabla?**
Comprometería totalmente la seguridad de las cuentas, ya que al estar en texto claro, el atacante podría ver las contraseñas sin ningún obstáculo y suplantar la identidad de los usuarios o robar su información personal.

---

## Generar una representación no reversible

1. **¿Son iguales?**No.
2. **Si no son iguales, ¿por qué?**Porque la instrucción incluye un componente aleatorio que genera un valor único (*salt*) en cada ejecución, provocando que el resultado final del hash sea distinto aunque la contraseña ingresada sea la misma.
3. **¿Qué función cumple `gen_salt()`?**Genera una cadena de caracteres aleatorios que se añade a la clave antes de procesarla, evitando que dos contraseñas iguales produzcan el mismo hash y protegiendo la información contra ataques basados en tablas precalculadas.
4. **¿Qué función cumple `crypt()`?**Recibe la contraseña en texto plano junto con la sal generada y procesa ambas con el algoritmo seleccionado para obtener una cadena de hash unidireccional.
5. **¿Esto es cifrado reversible?**
   No, se trata de una función unidireccional (*hashing*). No hay forma de revertir el proceso para obtener la clave original a partir del hash generado.

---

## Verificar una contraseña

1. **¿Qué resultado obtuviste con la contraseña correcta?**Un resultado afirmativo, confirmando que la contraseña ingresada coincide al recalcular el hash.
2. **¿Qué resultado obtuviste con la contraseña incorrecta?**Un resultado negativo, señalando que la clave introducida es errónea.
3. **¿Por qué no es necesario recuperar la contraseña original?**Porque la verificación consiste únicamente en procesar la contraseña introducida con la sal del registro y comparar si el hash generado concuerda con el almacenado.
4. **¿Por qué un hash no debe confundirse con cifrado?**
   Porque el cifrado es un proceso bidireccional diseñado para recuperar el texto original mediante una clave de descifrado, mientras que el hash es irreversible y se utiliza únicamente para validar integridad o autenticidad sin revelar el dato de origen.
