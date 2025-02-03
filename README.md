# COMPUTACION-EN-PARALELO-EN-PYTHON
  A continuación presento un ejemplo en Python que integra una red neuronal simple con técnicas de computación en paralelo para acelerar la inferencia. En este ejemplo utilizamos PyTorch para definir y entrenar el modelo y el módulo "concurrent.futures" para realizar la inferencia en paralelo dividiendo el conjunto de datos en “chunks”. Cada bloque se procesa en un hilo distinto, aprovechando que las operaciones en tensores (implementadas en C) liberan el GIL, lo que permite paralelismo efectivo en la inferencia.

Explicación y Técnicas de Optimización Aplicadas

    1. Carga de Datos en Paralelo:
Se utiliza DataLoader de PyTorch con el parámetro num_workers=2 para paralelizar la lectura y preparación de datos durante el entrenamiento, lo cual puede reducir significativamente el tiempo de espera en batches grandes.
       
    2. Inferencia Paralela con Threads:
La función inferencia_paralela divide el conjunto de datos en varios bloques (chunks) y utiliza ThreadPoolExecutor de concurrent.futures para procesarlos en paralelo. Esto es eficaz en PyTorch ya que, durante operaciones intensivas en cálculos (que se ejecutan en C), el Global Interpreter Lock (GIL) se libera, permitiendo que varios hilos se ejecuten concurrentemente.
       
    3. Uso de torch.no_grad():
Durante la inferencia, se desactiva el cálculo de gradientes con torch.no_grad(), lo que reduce la carga computacional y mejora la velocidad, ya que no se requiere el seguimiento de las operaciones para la retropropagación.
       
    4. Modularización y Comentarios:
Se han definido funciones específicas para cada tarea (generación de datos, entrenamiento, inferencia) para facilitar la comprensión, mantenimiento y escalabilidad del código. Cada sección está debidamente comentada para explicar el propósito y la optimización aplicada.
