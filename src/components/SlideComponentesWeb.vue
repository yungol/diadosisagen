<template>
  <div class="w-full h-full flex flex-col justify-center px-10 max-w-7xl mx-auto py-8 text-gray-200">
    
    <div class="mb-6 text-center">
      <h2 class="text-4xl md:text-5xl font-heading font-extrabold text-transparent bg-clip-text bg-gradient-to-r from-isagen-blue to-isagen-green mb-2 tracking-tight drop-shadow-lg">
        La Anatomía de una Aplicación
      </h2>
      <p class="text-lg text-gray-400 font-body">Cómo se construyen las interfaces modernas capa por capa</p>
    </div>

    <!-- Escenario Principal (Dark Tech / Silicon Valley Style) -->
    <div class="flex-grow bg-[#0f172a] rounded-3xl shadow-2xl relative overflow-hidden border border-gray-700/50 flex flex-col md:flex-row p-6 gap-6">
      
      <!-- Fondo de cuadrícula -->
      <div class="absolute inset-0 opacity-10 pointer-events-none" style="background-image: linear-gradient(#334155 1px, transparent 1px), linear-gradient(90deg, #334155 1px, transparent 1px); background-size: 40px 40px;"></div>

      <!-- Panel Izquierdo: Las 3 Capas (Explicación para Auditores) -->
      <div class="w-full md:w-5/12 flex flex-col justify-center space-y-4 z-10 relative">
        
        <!-- Tarjeta HTML -->
        <div :class="['p-4 rounded-xl border transition-all duration-500 backdrop-blur-sm', 
            activeLayer >= 1 ? 'bg-orange-500/10 border-orange-500/50 shadow-[0_0_15px_rgba(249,115,22,0.15)] transform translate-x-2' : 'bg-gray-800/50 border-gray-700 opacity-50']">
          <div class="flex items-center mb-2">
            <div :class="['w-8 h-8 rounded-lg flex items-center justify-center font-bold font-mono mr-3 transition-colors', activeLayer >= 1 ? 'bg-orange-500 text-white' : 'bg-gray-700 text-gray-500']">H</div>
            <h3 class="text-xl font-bold font-heading" :class="activeLayer >= 1 ? 'text-orange-400' : 'text-gray-500'">1. El Esqueleto (HTML)</h3>
          </div>
          <p class="text-sm text-gray-400 leading-relaxed font-body">Define la <strong>estructura y los datos</strong>. Para un auditor, aquí reside el contenido crudo, los formularios y la semántica de la información sin procesar.</p>
        </div>

        <!-- Tarjeta CSS -->
        <div :class="['p-4 rounded-xl border transition-all duration-500 backdrop-blur-sm', 
            activeLayer >= 2 ? 'bg-blue-500/10 border-blue-500/50 shadow-[0_0_15px_rgba(59,130,246,0.15)] transform translate-x-2' : 'bg-gray-800/50 border-gray-700 opacity-50']">
          <div class="flex items-center mb-2">
            <div :class="['w-8 h-8 rounded-lg flex items-center justify-center font-bold font-mono mr-3 transition-colors', activeLayer >= 2 ? 'bg-blue-500 text-white' : 'bg-gray-700 text-gray-500']">C</div>
            <h3 class="text-xl font-bold font-heading" :class="activeLayer >= 2 ? 'text-blue-400' : 'text-gray-500'">2. La Apariencia (CSS)</h3>
          </div>
          <p class="text-sm text-gray-400 leading-relaxed font-body">Controla el <strong>diseño visual y la adaptabilidad</strong>. Transforma el esqueleto en una interfaz profesional, oculta elementos y guía la atención del usuario.</p>
        </div>

        <!-- Tarjeta JS -->
        <div :class="['p-4 rounded-xl border transition-all duration-500 backdrop-blur-sm', 
            activeLayer >= 3 ? 'bg-yellow-400/10 border-yellow-400/50 shadow-[0_0_15px_rgba(250,204,21,0.15)] transform translate-x-2' : 'bg-gray-800/50 border-gray-700 opacity-50']">
          <div class="flex items-center mb-2">
            <div :class="['w-8 h-8 rounded-lg flex items-center justify-center font-bold font-mono text-black mr-3 transition-colors', activeLayer >= 3 ? 'bg-yellow-400' : 'bg-gray-700 text-gray-500']">J</div>
            <h3 class="text-xl font-bold font-heading" :class="activeLayer >= 3 ? 'text-yellow-400' : 'text-gray-500'">3. El Cerebro (JavaScript)</h3>
          </div>
          <p class="text-sm text-gray-400 leading-relaxed font-body">Aporta <strong>lógica, seguridad e interacción</strong>. Conecta con bases de datos, valida permisos, procesa transacciones y hace que la app cobre vida.</p>
        </div>

      </div>

      <!-- Panel Derecho: El Navegador / Preview -->
      <div class="w-full md:w-7/12 relative flex items-center justify-center z-10 perspective-1000">
        
        <!-- Ventana del Navegador Ficticio -->
        <div :class="['w-full max-w-md bg-white rounded-xl overflow-hidden transition-all duration-1000 transform', 
             activeLayer === 0 ? 'opacity-20 scale-95 grayscale' : 'opacity-100 scale-100',
             activeLayer >= 2 ? 'shadow-[0_20px_50px_rgba(0,0,0,0.5)]' : 'border-2 border-dashed border-gray-400 shadow-none']">
          
          <!-- Barra superior del navegador -->
          <div :class="['px-4 py-2 flex items-center space-x-2 border-b transition-colors duration-1000', 
               activeLayer >= 2 ? 'bg-slate-100 border-slate-200' : 'bg-transparent border-gray-300']">
            <div :class="['w-3 h-3 rounded-full transition-colors duration-1000', activeLayer >= 2 ? 'bg-red-400' : 'bg-gray-300']"></div>
            <div :class="['w-3 h-3 rounded-full transition-colors duration-1000', activeLayer >= 2 ? 'bg-yellow-400' : 'bg-gray-300']"></div>
            <div :class="['w-3 h-3 rounded-full transition-colors duration-1000', activeLayer >= 2 ? 'bg-green-400' : 'bg-gray-300']"></div>
            <div :class="['ml-4 flex-grow h-4 rounded transition-all duration-1000', activeLayer >= 2 ? 'bg-white shadow-sm' : 'bg-gray-200']"></div>
          </div>

          <!-- Contenido de la Web Ficticia -->
          <div class="p-6 relative h-64">
            
            <!-- CAPA 1: HTML (Estructura cruda) -->
            <div v-if="activeLayer === 1" class="absolute inset-0 p-6 font-serif text-black">
              <h1 class="text-2xl mb-4 underline">Dashboard Financiero</h1>
              <ul>
                <li>Usuario: Admin</li>
                <li>Balance: $45,000</li>
              </ul>
              <br>
              <button class="border border-black p-1">Actualizar Datos</button>
              <br><br>
              <table class="border border-black w-full text-sm">
                <tr><th class="border border-black">Mes</th><th class="border border-black">Ingreso</th></tr>
                <tr><td class="border border-black">Ene</td><td class="border border-black">100</td></tr>
              </table>
            </div>

            <!-- CAPA 2 & 3: CSS y JS -->
            <div v-if="activeLayer >= 2" class="absolute inset-0 p-6 bg-slate-50 font-sans transition-opacity duration-1000 text-slate-800 flex flex-col">
              
              <div class="flex justify-between items-center mb-6">
                <div>
                  <h1 class="text-xl font-bold text-slate-800 tracking-tight">Dashboard <span class="text-blue-600">Pro</span></h1>
                  <p class="text-xs text-slate-500">Bienvenido de nuevo, Admin</p>
                </div>
                <!-- Avatar -->
                <div class="w-10 h-10 rounded-full bg-gradient-to-tr from-blue-500 to-purple-500 shadow-md"></div>
              </div>

              <!-- Tarjeta de Balance -->
              <div class="bg-white p-4 rounded-xl shadow-sm border border-slate-100 mb-4 relative overflow-hidden">
                <div class="text-xs text-slate-400 uppercase font-semibold mb-1">Balance Total</div>
                <div class="text-3xl font-bold text-slate-800">
                  $45,000<span v-if="activeLayer >= 3" class="text-green-500 text-sm ml-2 animate-bounce inline-block">↑ 12%</span>
                </div>
                
                <!-- Decoración CSS -->
                <div class="absolute -right-4 -top-4 w-16 h-16 bg-blue-50 rounded-full opacity-50 pointer-events-none"></div>
              </div>

              <!-- Botón (Interactivo solo en Capa 3) -->
              <div class="mt-auto">
                <button 
                  @click="simulateDataFetch"
                  :class="['w-full py-2.5 rounded-lg font-semibold text-sm transition-all flex justify-center items-center', 
                   activeLayer >= 3 ? 'bg-blue-600 text-white shadow-lg hover:bg-blue-700 hover:shadow-xl cursor-pointer' : 'bg-slate-200 text-slate-500 cursor-default']"
                >
                  <svg v-if="isFetching && activeLayer >= 3" class="animate-spin -ml-1 mr-2 h-4 w-4 text-white" fill="none" viewBox="0 0 24 24"><circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle><path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path></svg>
                  <span v-if="!isFetching || activeLayer < 3">Actualizar Datos</span>
                  <span v-else>Conectando al servidor...</span>
                </button>
              </div>

              <!-- Partículas JS (Solo en Capa 3) -->
              <div v-if="activeLayer >= 3 && isFetching" class="absolute inset-0 pointer-events-none overflow-hidden rounded-b-xl z-50">
                 <div class="absolute w-2 h-2 bg-yellow-400 rounded-full blur-[1px] top-1/2 left-1/4 animate-ping"></div>
                 <div class="absolute w-2 h-2 bg-blue-400 rounded-full blur-[1px] top-1/3 left-3/4 animate-ping" style="animation-delay: 0.2s"></div>
                 <div class="absolute w-2 h-2 bg-green-400 rounded-full blur-[1px] bottom-1/4 left-1/2 animate-ping" style="animation-delay: 0.4s"></div>
              </div>

            </div>

          </div>
        </div>

        <!-- Líneas de código flotantes (Efecto Matrix/Tech) -->
        <div v-if="activeLayer >= 1" class="absolute inset-0 pointer-events-none z-0 overflow-hidden opacity-70">
           <pre v-if="activeLayer === 1" class="text-orange-400 text-base font-mono absolute top-10 left-4 animate-pulse drop-shadow-md">&lt;div id="app"&gt;<br>  &lt;h1&gt;Dashboard&lt;/h1&gt;<br>&lt;/div&gt;</pre>
           <pre v-if="activeLayer === 2" class="text-blue-400 text-base font-mono absolute bottom-10 right-4 animate-pulse drop-shadow-md">.card {<br>  border-radius: 12px;<br>  box-shadow: 0 4px 6px rgba(0,0,0,0.1);<br>}</pre>
           <pre v-if="activeLayer === 3" class="text-yellow-400 text-base font-mono absolute top-4 right-4 animate-pulse drop-shadow-md">async function fetchData() {<br>  const res = await api.get('/stats');<br>  updateDOM(res.data);<br>}</pre>
        </div>

      </div>

    </div>

    <!-- Controles Inferiores -->
    <div class="mt-6 flex justify-center items-center space-x-4">
      <button 
        v-if="activeLayer < 3"
        @click="nextLayer" 
        :disabled="isAnimating"
        class="px-8 py-3 bg-gradient-to-r from-blue-600 to-indigo-600 hover:from-blue-500 hover:to-indigo-500 text-white font-bold rounded-full shadow-lg transition-all disabled:opacity-50 flex items-center shadow-[0_0_20px_rgba(79,70,229,0.4)]"
      >
        <span class="mr-2">{{ getButtonText() }}</span>
        <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"></path></svg>
      </button>
      
      <button v-if="activeLayer === 3" @click="resetLayers" class="px-8 py-3 bg-gray-800 hover:bg-gray-700 text-white font-bold rounded-full shadow-lg transition-all flex items-center border border-gray-600">
        <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15"></path></svg>
        Reiniciar Construcción
      </button>
    </div>

  </div>
</template>

<script>
export default {
  name: 'SlideComponentesWeb',
  data() {
    return {
      activeLayer: 0,
      isAnimating: false,
      isFetching: false
    }
  },
  methods: {
    delay(ms) {
      return new Promise(resolve => setTimeout(resolve, ms));
    },
    getButtonText() {
      if (this.activeLayer === 0) return 'Inyectar Código HTML';
      if (this.activeLayer === 1) return 'Aplicar Estilos CSS';
      if (this.activeLayer === 2) return 'Activar Lógica JavaScript';
      return '';
    },
    async nextLayer() {
      if (this.isAnimating || this.activeLayer >= 3) return;
      this.isAnimating = true;
      this.activeLayer++;
      await this.delay(600); // Tiempo de la transición CSS
      this.isAnimating = false;
    },
    resetLayers() {
      this.activeLayer = 0;
      this.isFetching = false;
    },
    async simulateDataFetch() {
      if (this.activeLayer < 3 || this.isFetching) return;
      this.isFetching = true;
      await this.delay(1500); // Simulamos llamada al servidor
      this.isFetching = false;
    }
  }
}
</script>

<style scoped>
.perspective-1000 {
  perspective: 1000px;
}
</style>