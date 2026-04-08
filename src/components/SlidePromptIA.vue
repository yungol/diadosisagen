<template>
  <div class="h-full w-full flex flex-col justify-center items-center p-10 text-center">
    <!-- Encabezado -->
    <h2 class="text-4xl md:text-5xl font-heading font-extrabold text-isagen-blue mb-10">
      ¡Ahora le toca a la IA!
    </h2>

    <!-- Contenedor Principal -->
    <div class="w-full max-w-5xl bg-white p-8 md:p-10 rounded-2xl shadow-xl border-t-8 border-isagen-green flex flex-col items-center gap-8">
      
      <!-- Instrucción superior -->
      <div class="flex items-start space-x-3 w-full text-left">
        <span class="bg-isagen-blue text-white rounded-full w-8 h-8 flex-shrink-0 flex items-center justify-center font-bold text-xl mt-0.5">1</span>
        <p class="text-lg text-gray-700">
          Ve a tu IA favorita (ChatGPT, Gemini, Copilot…) y <strong class="text-gray-900">copia y pega exactamente este prompt</strong>:
        </p>
      </div>

      <!-- Bloque del Prompt + QR lado a lado -->
      <div class="flex flex-col md:flex-row w-full gap-6 items-center">

        <!-- Bloque del Prompt -->
        <div class="relative flex-1 w-full">
          <!-- Etiqueta del bloque -->
          <span class="absolute -top-3.5 left-4 bg-isagen-dark text-white text-xs font-mono px-3 py-0.5 rounded-full tracking-widest uppercase">
            Prompt
          </span>
          <div class="bg-gray-900 text-gray-100 font-mono text-xl md:text-2xl p-8 pt-9 rounded-xl shadow-inner leading-relaxed text-left">
            dame un&nbsp;
            <span class="bg-isagen-green text-isagen-dark font-extrabold px-2 py-0.5 rounded">html autocontenido</span>
            &nbsp;que explique de forma didáctica que son los controles SOX en auditoría utilizando&nbsp;
            <span class="bg-isagen-blue text-white font-extrabold px-2 py-0.5 rounded">tailwind</span>
            &nbsp;para los estilos
          </div>
        </div>

        <!-- QR Code -->
        <div class="flex flex-col items-center gap-2 flex-shrink-0">
          <div class="bg-white p-3 rounded-xl shadow-md border-2 border-isagen-green">
            <img v-if="qrDataUrl" :src="qrDataUrl" alt="QR del prompt" class="w-36 h-36 md:w-44 md:h-44" />
            <div v-else class="w-36 h-36 md:w-44 md:h-44 flex items-center justify-center text-gray-400 text-sm">
              Generando QR…
            </div>
          </div>
          <p class="text-xs text-gray-500 font-medium">Escanea para copiar<br>el prompt en tu celular</p>
        </div>

      </div>

      <!-- Instrucción inferior -->
      <div class="flex items-start space-x-3 w-full text-left">
        <span class="bg-isagen-green text-isagen-dark rounded-full w-8 h-8 flex-shrink-0 flex items-center justify-center font-bold text-xl mt-0.5">2</span>
        <p class="text-lg text-gray-700">
          Copia el código HTML que te devuelva, pégalo en el <strong class="text-gray-900">Bloc de notas</strong> y guárdalo como <code class="bg-gray-100 px-2 py-0.5 rounded text-isagen-blue font-mono border border-gray-300 text-base">soc.html</code>.
          Luego ábrelo en el navegador y ¡listo!
        </p>
      </div>

      <!-- Nota aclaratoria -->
      <p class="text-sm text-gray-500 italic bg-yellow-50 w-full p-3 rounded border border-yellow-200 text-left">
        <strong>¿Por qué esas palabras?</strong>
        &nbsp;"<span class="font-semibold text-isagen-dark">html autocontenido</span>" le dice a la IA que todo el código debe ir en un solo archivo.
        &nbsp;"<span class="font-semibold text-isagen-blue">tailwind</span>" le indica el sistema de estilos que debe usar, igual que en este taller.
      </p>

    </div>
  </div>
</template>

<script>
import QRCode from 'qrcode'

const PROMPT_TEXT = 'dame un html autocontenido que explique de forma didáctica que son los controles SOX en auditoría utilizando tailwind para los estilos'

export default {
  name: 'SlidePromptIA',
  data() {
    return {
      qrDataUrl: null
    }
  },
  mounted() {
    QRCode.toDataURL(PROMPT_TEXT, {
      width: 256,
      margin: 2,
      color: {
        dark: '#003366',
        light: '#ffffff'
      }
    }).then(url => {
      this.qrDataUrl = url
    }).catch(err => {
      console.error('Error generando QR:', err)
    })
  }
}
</script>
