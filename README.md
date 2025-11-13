# 🌐 StressMonitor - Sistema IoT de Monitoramento de Estresse no Home Office

## 📘 Descrição do Projeto
O **StressMonitor** é uma solução **IoT baseada em ESP32**, desenvolvida para promover o **bem-estar e a produtividade de profissionais em home office**.  
Através de sensores simulados no **Wokwi**, o sistema estima o **nível de estresse** do usuário, envia os dados via **MQTT** para um dashboard remoto e emite **alertas automáticos** sugerindo pausas quando o nível de estresse ultrapassa limites pré-definidos.

O projeto integra os conceitos de **Edge Computing**, **automação inteligente** e **Internet das Coisas (IoT)**, sendo parte da  
📚 **Global Solution 2025 – Edge Computing & Computer Systems**, cujo tema é **“O Futuro do Trabalho”**.

---

## 🧠 Problema
Com o aumento do trabalho remoto, muitos profissionais enfrentam **altos níveis de estresse e fadiga mental**.  
Fatores como **longas jornadas**, **falta de pausas** e **ambientes mal ajustados** contribuem para a queda de produtividade e problemas de saúde.  
Sem um sistema de feedback automático, os sinais de sobrecarga passam despercebidos.

---

## 💡 Solução Proposta
O **StressMonitor** oferece uma **abordagem automatizada e inteligente** para o monitoramento do estresse.  
Através de sensores simulados, ele:
- Coleta dados de frequência cardíaca, ruído e movimento (via MPU6050);
- Calcula um **Stress Score (0 a 100)** com base nesses parâmetros;
- Publica os dados via **MQTT** para um dashboard remoto (Node-RED ou ThingSpeak);
- Emite **alertas locais** (LED e buzzer) quando detecta alto estresse;
- Permite **confirmação da pausa** através de um botão físico.

Com isso, o sistema demonstra como a **tecnologia pode contribuir para o bem-estar no trabalho digital**, automatizando decisões e promovendo pausas conscientes.

---

## 🧩 Componentes Utilizados
| Componente | Função | Simulado no Wokwi |
|-------------|--------|-------------------|
| **ESP32 DevKit** | Processamento e comunicação MQTT | ✅ |
| **Potenciômetro 1** | Simula batimentos cardíacos | ✅ |
| **Potenciômetro 2** | Simula ruído ambiental | ✅ |
| **MPU6050** | Detecta movimento e postura (atividade) | ✅ |
| **Buzzer** | Alerta sonoro de pausa | ✅ |
| **LED (vermelho)** | Indica status de alerta | ✅ |
| **Botão (push)** | Confirma pausa | ✅ |
| **OLED SSD1306 (opcional)** | Exibe score e status local | ✅ |

---

## ⚙️ Diagrama (Circuito Wokwi)
### Conexões principais
- **Potenciômetro 1** → `GPIO34` → frequência cardíaca simulada  
- **Potenciômetro 2** → `GPIO35` → ruído ambiental  
- **MPU6050** → SDA `21`, SCL `22`  
- **Buzzer** → `GPIO25`  
- **LED vermelho** → `GPIO26`  
- **Botão** → `GPIO0` (com `INPUT_PULLUP`)  
- **OLED (opcional)** → SDA `21`, SCL `22`

🔗 [**Abrir simulação no Wokwi**](#) *(link será adicionado após montagem do circuito)*

---

## ☁️ Comunicação MQTT
O sistema utiliza o **protocolo MQTT** para publicar dados e receber comandos de controle.

**Broker de teste:** `test.mosquitto.org`

| Tipo | Tópico | Descrição |
|------|--------|------------|
| **Publish** | `homeoffice/marcello/stress` | Envia o score de estresse e dados dos sensores |
| **Subscribe** | `homeoffice/marcello/cmd` | Recebe comandos externos (ex: pausa, reset) |

**Exemplo de payload publicado (JSON):**
```json
{
  "timestamp": "2025-11-12T20:00:00Z",
  "score": 72,
  "heartrate": 92,
  "noise": 48,
  "movement": 0.82,
  "action": "PAUSE_SUGGESTED"
}
