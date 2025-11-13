# 🌐 StressMonitor - Sistema IoT de Monitoramento de Estresse no Home Office

## 📘 Descrição do Projeto
O **StressMonitor** é uma solução baseada em **ESP32** que visa promover o bem-estar e a produtividade de profissionais em **home office**, utilizando **sensores IoT** para estimar o nível de estresse e sugerir **pausas automáticas** quando necessário.  

O projeto faz parte da **Global Solution 2025 – Edge Computing & Computer Systems**, cujo tema é **“O Futuro do Trabalho”**, e demonstra como a **automação e a Internet das Coisas (IoT)** podem contribuir para ambientes de trabalho mais saudáveis e sustentáveis.

---

## 🧠 Problema
Com o avanço do trabalho remoto, muitos profissionais enfrentam **altos níveis de estresse** devido a longas horas de tela, má postura e falta de pausas adequadas.  
Sem um sistema de monitoramento ou feedback, o colaborador tende a ignorar sinais físicos e mentais de fadiga, impactando negativamente sua **saúde** e **produtividade**.

---

## 💡 Solução Proposta
O **StressMonitor** propõe um **dispositivo IoT inteligente** que:
- Monitora indicadores indiretos de estresse, como **frequência cardíaca simulada**, **nível de movimento** e **ruído ambiental**;
- Calcula um **“Stress Score”** (0 a 100) com base nesses dados;
- Envia informações via **MQTT** para um dashboard remoto;
- Emite **alertas locais** (LED/Buzzer) quando o nível de estresse ultrapassa um limite, sugerindo pausas;
- Permite confirmação da pausa via botão físico.

---

## 🧩 Componentes Utilizados
| Componente | Função | Simulação no Wokwi |
|-------------|--------|-------------------|
| ESP32 DevKit | Unidade de processamento e comunicação | ✅ |
| 2x Potenciômetros | Simulam frequência cardíaca e ruído | ✅ |
| MPU6050 (opcional) | Detecta movimento/postura | ✅ |
| Buzzer | Alerta de pausa | ✅ |
| Botão | Confirma pausa ou adia alerta | ✅ |
| (Opcional) OLED SSD1306 | Exibe score e mensagens locais | ✅ |

---

## ⚙️ Diagrama (Circuito Wokwi)
### Conexões principais
- **Potenciômetro 1** → pino `34` (frequência cardíaca simulada)  
- **Potenciômetro 2** → pino `35` (nível de ruído)  
- **MPU6050** → SDA `21`, SCL `22`, VCC `3.3V`, GND `GND`  
- **Buzzer** → pino `25`  
- **Botão** → pino `0` (com `INPUT_PULLUP`)  
- **OLED (opcional)** → SDA `21`, SCL `22`

🔗 [**Abrir simulação no Wokwi**](#) *(link será inserido após montagem)*

---

## ☁️ Comunicação MQTT
O sistema envia e recebe dados via **protocolo MQTT**.  
Broker de teste: `test.mosquitto.org`  

**Tópicos utilizados:**
| Tipo | Tópico | Descrição |
|------|--------|------------|
| Publish | `homeoffice/marcello/stress` | Envia dados do nível de estresse |
| Subscribe | `homeoffice/marcello/cmd` | Recebe comandos (ex: reset, pausa manual) |

**Payload (JSON):**
```json
{
  "timestamp": "2025-11-12T20:00:00Z",
  "score": 72,
  "heartrate": 92,
  "immobility": 0.8,
  "action": "PAUSE_SUGGESTED"
}
