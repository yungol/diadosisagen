<template>
  <div class="h-full w-full flex flex-col justify-center items-center p-10 text-center">
    <!-- Encabezado -->
    <h2 class="text-4xl md:text-5xl font-heading font-extrabold text-isagen-blue mb-10">
      ¡Tu Primer "Hola Mundo"!
    </h2>

    <!-- Contenedor Principal -->
    <div class="w-full max-w-5xl bg-white p-8 md:p-10 rounded-2xl shadow-xl border-t-8 border-isagen-green flex flex-col items-center">
      <div class="grid grid-cols-1 md:grid-cols-2 gap-10 w-full">
        
        <!-- Columna 1: Instrucciones Bloc de Notas -->
        <div class="flex flex-col text-left space-y-5">
          <div class="flex items-center space-x-3 border-b-2 border-gray-200 pb-3">
            <span class="bg-isagen-blue text-white rounded-full w-8 h-8 flex items-center justify-center font-bold text-xl">1</span>
            <h3 class="text-2xl font-bold text-gray-800">Crea tu página web</h3>
          </div>
          <ul class="list-disc list-inside text-lg text-gray-700 space-y-3">
            <li>Abre el <strong>Bloc de notas</strong> en tu computador.</li>
            <li>Escribe simplemente el texto: <br> <code class="bg-gray-100 px-3 py-1 rounded text-isagen-blue font-mono border border-gray-300 shadow-sm inline-block mt-2">Hola Mundo</code></li>
            <li>Guarda el archivo en tu escritorio (Archivo &gt; Guardar como...) con este nombre exacto:</li>
          </ul>
          <div class="bg-gray-800 text-white font-mono p-4 rounded-lg shadow-inner text-center text-xl font-bold tracking-wider">
            index.html
          </div>
          <p class="text-sm text-gray-500 italic bg-yellow-50 p-3 rounded border border-yellow-200">
            <strong>Tip:</strong> Asegúrate de que el "Tipo" esté configurado en "Todos los archivos" antes de guardar para que no quede como index.html.txt.
          </p>
        </div>

        <!-- Columna 2: Consola del Navegador -->
        <div class="flex flex-col text-left space-y-5">
          <div class="flex items-center space-x-3 border-b-2 border-gray-200 pb-3">
            <span class="bg-isagen-green text-white rounded-full w-8 h-8 flex items-center justify-center font-bold text-xl">2</span>
            <h3 class="text-2xl font-bold text-gray-800">Magia con la Consola</h3>
          </div>
          <ul class="list-disc list-inside text-lg text-gray-700 space-y-3">
            <li>Abre tu nuevo archivo <code class="font-bold text-isagen-blue">index.html</code> en el navegador.</li>
            <li>Presiona la tecla <strong>F12</strong> y ve a la pestaña <strong>Consola</strong> (o Console).</li>
            <li>Copia, pega y presiona <strong>Enter</strong> con estos dos códigos para cambiar el diseño de la página:</li>
          </ul>
          
          <div class="space-y-3 mt-4">
            <div class="relative">
              <span class="absolute -top-3 left-3 bg-gray-600 text-white text-xs px-2 py-0.5 rounded">Cambiar fondo</span>
              <div class="bg-gray-800 text-green-400 font-mono p-4 pt-5 rounded-lg shadow-inner text-sm overflow-x-auto">
                document.body.style.backgroundColor = "black";
              </div>
            </div>
            
            <div class="relative">
              <span class="absolute -top-3 left-3 bg-gray-600 text-white text-xs px-2 py-0.5 rounded">Cambiar color de texto</span>
              <div class="bg-gray-800 text-green-400 font-mono p-4 pt-5 rounded-lg shadow-inner text-sm overflow-x-auto">
                document.body.style.color = "lime";
              </div>
            </div>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SlideHelloWorld'
}
</script>
