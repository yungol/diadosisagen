<template>
  <div class="w-full h-full flex flex-col justify-center px-10 max-w-7xl mx-auto py-8">
    
    <div class="mb-6 text-center">
      <h2 class="text-4xl md:text-5xl font-heading font-extrabold text-isagen-blue mb-2 tracking-tight">
        El Viaje de tu Petición Web
      </h2>
      <p class="text-lg text-gray-500 font-body">Lo que realmente sucede en milisegundos cuando presionas <strong>Enter</strong></p>
    </div>

    <!-- Escenario Principal (Estilo Dark Tech) -->
    <div class="flex-grow bg-gray-900 rounded-3xl shadow-2xl relative overflow-hidden border border-gray-700 flex flex-col justify-between p-6">
      
      <!-- Fondo de cuadrícula tecnológica -->
      <div class="absolute inset-0 opacity-10 pointer-events-none" style="background-image: linear-gradient(#374151 1px, transparent 1px), linear-gradient(90deg, #374151 1px, transparent 1px); background-size: 30px 30px;"></div>

      <!-- Líneas de Conexión (Fondo) -->
      <svg class="absolute inset-0 w-full h-full pointer-events-none z-0">
        <!-- Línea Base: Usuario a DNS -->
        <line x1="15%" y1="75%" x2="50%" y2="25%" stroke="rgba(255,255,255,0.05)" stroke-width="2" stroke-dasharray="4 4" />
        <!-- Línea Base: Usuario a Servidor -->
        <line x1="15%" y1="75%" x2="85%" y2="75%" stroke="rgba(255,255,255,0.05)" stroke-width="2" stroke-dasharray="4 4" />

        <!-- Animación de flujo de datos: Usuario <-> DNS -->
        <line v-if="step === 2 || step === 4" x1="15%" y1="75%" x2="50%" y2="25%" stroke="#00A3E0" stroke-width="3" stroke-dasharray="8 8" opacity="0.8">
          <animate attributeName="stroke-dashoffset" :from="step === 2 ? '32' : '0'" :to="step === 2 ? '0' : '32'" dur="0.8s" repeatCount="indefinite" />
        </line>

        <!-- Animación de flujo de datos: Usuario <-> Servidor -->
        <line v-if="step === 5 || step === 7" x1="15%" y1="75%" x2="85%" y2="75%" :stroke="step === 5 ? '#FBBF24' : '#78BE20'" stroke-width="3" stroke-dasharray="8 8" opacity="0.8">
          <animate attributeName="stroke-dashoffset" :from="step === 5 ? '32' : '0'" :to="step === 5 ? '0' : '32'" dur="0.8s" repeatCount="indefinite" />
        </line>
      </svg>

      <!-- El Paquete de Datos (El que se mueve) -->
      <div 
        v-if="packet.show"
        class="absolute z-50 flex items-center justify-center transition-all duration-1000 ease-in-out transform -translate-x-1/2 -translate-y-1/2"
        :style="{ left: packet.left, top: packet.top }"
      >
        <div class="relative">
          <div :class="`absolute inset-0 blur-md rounded-full ${packet.color}`"></div>
          <div :class="`relative w-4 h-4 rounded-full ${packet.color} shadow-lg`"></div>
        </div>
        <div class="absolute top-6 whitespace-nowrap bg-gray-800 border border-gray-600 text-white text-xs px-3 py-1 rounded-full shadow-xl">
          {{ packet.text }}
        </div>
      </div>

      <!-- NODO 1: Usuario (Abajo Izquierda) -->
      <div class="absolute z-10 w-64" style="left: 15%; top: 75%; transform: translate(-50%, -50%);">
        <div class="bg-gray-800 rounded-xl p-4 border border-gray-600 shadow-2xl relative overflow-hidden">
          <div class="flex items-center space-x-2 mb-3 border-b border-gray-700 pb-2">
            <div class="w-3 h-3 rounded-full bg-red-500"></div>
            <div class="w-3 h-3 rounded-full bg-yellow-500"></div>
            <div class="w-3 h-3 rounded-full bg-green-500"></div>
            <span class="text-xs text-gray-400 ml-2 font-mono">Navegador</span>
          </div>
          
          <div class="bg-gray-900 rounded border border-gray-700 p-2 font-mono text-sm h-10 flex items-center">
            <span class="text-gray-500 mr-2">https://</span>
            <span class="text-green-400 font-bold">{{ urlText }}</span>
            <span v-if="step === 1 || step === 0" class="animate-pulse w-1 h-4 bg-white ml-1"></span>
          </div>

          <div class="mt-4 h-24 bg-gray-900 rounded flex items-center justify-center border border-gray-700">
            <span v-if="browserStatus === 'empty'" class="text-gray-600 text-sm">Esperando acción...</span>
            <span v-if="browserStatus === 'loading'" class="text-isagen-green animate-pulse text-sm">Cargando...</span>
            <div v-if="browserStatus === 'loaded'" class="text-center">
              <span class="text-2xl">🎉</span>
              <p class="text-green-400 text-xs mt-1 font-bold">¡App Cargada!</p>
            </div>
          </div>
        </div>
        <div class="text-center mt-3 text-white font-bold font-heading">1. Tú (El Auditor)</div>
      </div>

      <!-- NODO 2: DNS (Arriba Centro) -->
      <div class="absolute z-10 w-56" style="left: 50%; top: 25%; transform: translate(-50%, -50%);">
        <div :class="['rounded-xl p-4 border shadow-2xl transition-all duration-500', 
            serverStatus === 'resolving' ? 'bg-isagen-blue bg-opacity-20 border-isagen-blue shadow-[0_0_30px_rgba(0,163,224,0.3)]' : 'bg-gray-800 border-gray-600']">
          <div class="text-center mb-2">
            <svg class="w-12 h-12 mx-auto text-isagen-blue mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M21 12a9 9 0 01-9 9m9-9a9 9 0 00-9-9m9 9H3m9 9a9 9 0 01-9-9m9 9c1.657 0 3-4.03 3-9s-1.343-9-3-9m0 18c-1.657 0-3-4.03-3-9s1.343-9 3-9m-9 9a9 9 0 019-9"></path></svg>
            <span class="text-white font-bold">2. Servidor DNS</span>
            <p class="text-xs text-gray-400 mt-1">El Directorio Telefónico</p>
          </div>
          
          <div class="bg-gray-900 rounded p-2 text-xs font-mono h-16 flex flex-col justify-center overflow-hidden relative">
            <div v-if="serverStatus === 'resolving'" class="absolute inset-0 bg-isagen-blue opacity-10 animate-pulse"></div>
            <div v-if="serverStatus === 'resolving'" class="text-green-400 z-10 text-center">Buscando...</div>
            <div v-if="serverStatus === 'resolved'" class="z-10 flex flex-col items-center">
              <span class="text-gray-300">miauditor.com</span>
              <span class="text-isagen-blue font-bold">⬇ 192.168.45.10</span>
            </div>
          </div>
        </div>
      </div>

      <!-- NODO 3: El Servidor en USA (Abajo Derecha) -->
      <div class="absolute z-10 w-72" style="left: 85%; top: 75%; transform: translate(-50%, -50%);">
        <div :class="['rounded-xl p-5 border shadow-2xl transition-all duration-500 relative overflow-hidden', 
            serverStatus === 'processing' ? 'bg-isagen-green bg-opacity-20 border-isagen-green shadow-[0_0_30px_rgba(120,190,32,0.3)]' : 'bg-gray-800 border-gray-600']">
          
          <!-- Mapa de USA pixelado (puntos) de fondo -->
          <svg class="absolute right-0 bottom-0 w-64 h-64 opacity-20 text-isagen-green transform translate-x-12 translate-y-12 z-0" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
            <defs>
              <pattern id="dot-grid" width="3" height="3" patternUnits="userSpaceOnUse">
                <circle cx="1.5" cy="1.5" r="1.2" fill="currentColor" opacity="0.8"/>
              </pattern>
            </defs>
            <!-- Contorno simplificado y abstracto de Norteamérica -->
            <polygon points="15,30 35,25 50,28 70,20 85,35 90,55 80,65 75,85 65,75 55,65 45,70 35,85 20,60 10,40" fill="url(#dot-grid)" />
            <!-- Pequeños puntos sueltos para dar efecto tecnológico -->
            <circle cx="85" cy="40" r="1.5" fill="currentColor" />
            <circle cx="80" cy="45" r="1.5" fill="currentColor" />
            <circle cx="75" cy="50" r="1.5" fill="currentColor" />
            <circle cx="70" cy="55" r="1.5" fill="currentColor" />
            <circle cx="65" cy="60" r="1.5" fill="currentColor" />
          </svg>

          <div class="flex flex-col items-center space-y-4 relative z-10">
            <div class="relative">
              <svg class="w-16 h-16 text-isagen-green" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M5 12h14M5 12a2 2 0 01-2-2V6a2 2 0 012-2h14a2 2 0 012 2v4a2 2 0 01-2 2M5 12a2 2 0 00-2 2v4a2 2 0 002 2h14a2 2 0 002-2v-4a2 2 0 00-2-2m-2-4h.01M17 16h.01"></path></svg>
              <!-- Ping/Beacon location -->
              <div v-if="serverStatus === 'processing'" class="absolute top-2 right-2 w-3 h-3 bg-red-500 rounded-full animate-ping"></div>
              <div class="absolute top-2 right-2 w-3 h-3 bg-red-500 rounded-full"></div>
            </div>
            <div class="text-center">
              <span class="text-white font-bold block text-lg">3. "La Nube"</span>
              <span class="text-xs text-gray-400 block">Data Center (EE.UU.)</span>
              <span class="text-xs font-mono bg-gray-900 text-green-400 px-2 py-1 rounded mt-1 inline-block">192.168.45.10</span>
            </div>
          </div>
          
          <div class="mt-4 bg-gray-900 rounded p-2 text-xs font-mono h-12 flex items-center justify-center relative z-10">
             <span v-if="serverStatus !== 'processing'" class="text-gray-600">Servidor en espera...</span>
             <span v-if="serverStatus === 'processing'" class="text-isagen-green animate-pulse">Generando HTML/JS/CSS...</span>
          </div>
        </div>
      </div>

    </div>

    <!-- Controles -->
    <div class="mt-6 flex justify-center items-center space-x-4">
      <button 
        @click="runSimulation" 
        :disabled="isAnimating"
        class="px-8 py-3 bg-isagen-green hover:bg-opacity-80 text-white font-bold rounded-full shadow-lg transition-all disabled:opacity-50 disabled:cursor-not-allowed flex items-center"
      >
        <svg v-if="!isAnimating" class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14.752 11.168l-3.197-2.132A1 1 0 0010 9.87v4.263a1 1 0 001.555.832l3.197-2.132a1 1 0 000-1.664z"></path><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
        <svg v-else class="animate-spin w-5 h-5 mr-2" fill="none" viewBox="0 0 24 24"><circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle><path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path></svg>
        {{ isAnimating ? 'Simulando viaje...' : 'Simular Petición Web' }}
      </button>
      
      <button v-if="step === 8" @click="resetSimulation" class="px-4 py-3 text-gray-500 hover:text-gray-700 underline text-sm font-body">
        Reiniciar
      </button>
    </div>

  </div>
</template>

<script>
export default {
  name: 'SlideComoFuncionaWeb',
  data() {
    return {
      step: 0,
      isAnimating: false,
      urlText: '',
      fullUrl: 'miauditor.com',
      browserStatus: 'empty', // empty, loading, loaded
      serverStatus: 'idle', // idle, resolving, resolved, processing
      packet: {
        show: false,
        left: '15%',
        top: '75%',
        text: '',
        color: 'bg-blue-400'
      }
    }
  },
  methods: {
    delay(ms) {
      return new Promise(resolve => setTimeout(resolve, ms));
    },
    async typeUrl() {
      this.urlText = '';
      for (let i = 0; i < this.fullUrl.length; i++) {
        this.urlText += this.fullUrl.charAt(i);
        await this.delay(50); // Velocidad de tipeo
      }
    },
    resetSimulation() {
      this.step = 0;
      this.isAnimating = false;
      this.urlText = '';
      this.browserStatus = 'empty';
      this.serverStatus = 'idle';
      this.packet.show = false;
      this.packet.left = '15%';
      this.packet.top = '75%';
    },
    async runSimulation() {
      if (this.isAnimating) return;
      
      this.resetSimulation();
      this.isAnimating = true;

      // Paso 1: Escribir URL
      this.step = 1;
      await this.typeUrl();
      await this.delay(500);

      // Paso 2: Usuario a DNS
      this.step = 2;
      this.browserStatus = 'loading';
      this.packet.text = '¿IP de miauditor.com?';
      this.packet.color = 'bg-blue-400';
      this.packet.left = '15%';
      this.packet.top = '75%';
      this.packet.show = true;
      
      // Mover a DNS
      await this.delay(100); // Dar tiempo a Vue de renderizar el paquete
      this.packet.left = '50%';
      this.packet.top = '25%';
      
      await this.delay(1000); // Tiempo de viaje

      // Paso 3: DNS Resolviendo
      this.step = 3;
      this.serverStatus = 'resolving';
      this.packet.show = false; // Se esconde mientras el DNS piensa
      await this.delay(800);
      
      this.serverStatus = 'resolved';
      await this.delay(400);

      // Paso 4: DNS a Usuario
      this.step = 4;
      this.packet.text = 'IP: 192.168.45.10';
      this.packet.color = 'bg-isagen-blue';
      this.packet.show = true;
      this.packet.left = '15%';
      this.packet.top = '75%';
      
      await this.delay(1000); // Tiempo de viaje de regreso

      // Paso 5: Usuario a Servidor USA
      this.step = 5;
      this.packet.text = 'GET / (Quiero la página)';
      this.packet.color = 'bg-yellow-400';
      this.packet.left = '85%';
      this.packet.top = '75%';
      
      await this.delay(1000); // Tiempo de viaje por el océano

      // Paso 6: Servidor procesando
      this.step = 6;
      this.packet.show = false;
      this.serverStatus = 'processing';
      await this.delay(1200); // Generando la página

      // Paso 7: Servidor a Usuario
      this.step = 7;
      this.serverStatus = 'idle';
      this.packet.text = '<html>... (La Aplicación)';
      this.packet.color = 'bg-isagen-green';
      this.packet.left = '15%';
      this.packet.top = '75%';
      this.packet.show = true;

      await this.delay(1000); // Viaje de regreso con los datos

      // Paso 8: Fin
      this.step = 8;
      this.packet.show = false;
      this.browserStatus = 'loaded';
      this.isAnimating = false;
    }
  }
}
</script>