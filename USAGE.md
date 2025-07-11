# Usage Guide - Voice Bridge for Pathology

This guide covers daily usage of Voice Bridge for molecular pathology workflows, from basic operation to advanced features for hands-free microscopy.

## 🚀 Quick Start

### Starting Voice Bridge
```bash
# Method 1: Application Menu
# Click "Voice Bridge" icon in Applications → AudioVideo

# Method 2: Command Line
cd ~/voice-bridge-claude
./start_voice_bridge_gui.sh

# Method 3: Hotkey (after setup)
# Ctrl+Alt+V (if configured)
```

### System Status Verification
Upon startup, verify these indicators:
- **Status**: 🟢 Sistema listo
- **Log**: ✅ Azure Speech Services configurado correctamente
- **Dictionaries**: ✅ 95 términos médicos personalizados cargados
- **Audio**: TTS checkbox enabled for hands-free operation

## 🎤 Basic Voice Control

### Essential Hotkeys
- **Ctrl+Shift+V**: Start voice recognition
- **Ctrl+Shift+S**: Stop voice recognition
- **Ctrl+Shift+X**: Emergency stop (all recognition)

### Voice Confirmations
When TTS is enabled, you'll hear:
- **"Reconocimiento iniciado"**: Recognition started
- **"Reconocimiento detenido"**: Recognition stopped
- **"Recibido dictado con: [terms]"**: Dictation received with key medical terms
- **"Enviado a Claude"**: Automatically sent to Claude Desktop

## 🔬 Microscopy Workflow

### Typical Daily Session

#### 1. Setup Phase
```bash
# Start Voice Bridge
./start_voice_bridge_gui.sh

# Verify status
✅ Sistema listo
✅ 95 términos médicos cargados
✅ TTS habilitado

# Start Claude Desktop (for integration)
# Open Obsidian (for templates)
```

#### 2. Microscopy Analysis Phase
```
Pathologist: [Ctrl+Shift+V]
System: 🔊 "Reconocimiento iniciado"

Pathologist: "Observo en la biopsia de piel una hiperqueratosis marcada con células atípicas en la capa basal que muestran pleomorfismo nuclear y invasión focal de la dermis papilar compatible con carcinoma basocelular"

System: 🔊 "Recibido dictado con: carcinoma, pleomorfismo, invasión"
System: 🔊 "Enviado a Claude" (if auto-send enabled)

Claude: [Processing with templates...] "Perfect analysis. Do you observe vascular or perineural invasion? Need to evaluate surgical margins?"
```

#### 3. Documentation Phase
- **Automatic**: Claude processes with Obsidian templates
- **Manual**: Review and edit transcriptions
- **Export**: Save to medical records system

### Hands-Free Commands

#### Voice Status Commands
- **"Repetir transcripción"**: Reads last transcription
- **"Estado del sistema"**: System status report
- **"Enviar a Claude"**: Force manual sending

#### Medical Workflow Commands
- **"Nuevo caso [type]"**: Start new case documentation
- **"Agregar observación"**: Add to current case
- **"Finalizar informe"**: Complete and save report

## 🩺 Medical Dictation Patterns

### Optimized Dictation Types

#### 1. Histopathological Observations
**Pattern**: Clear, continuous medical observations
**Example**:
```
"Cortes histológicos de riñón donde destaca neoplasia maligna compuesta por células dispuestas en trabéculas y en acúmulos sólidos de citoplasma claro con núcleos irregulares algunos hipercromáticos de pleomorfismo moderado y algunos con nucléolo visibles a aumentos mayores la lesión compromete la cápsula renal sin sobrepasarla"
```

**Result**: Single continuous transcription with perfect medical terminology

#### 2. Diagnostic Classifications
**Pattern**: Structured diagnostic information
**Example**:
```
"Gastritis crónica moderada metaplasia intestinal incompleta antral leve clasificación uno de viena olga estadio cero olgim estadio uno protocolo de sydney"
```

**Result**: Accurate classification with proper medical scores

#### 3. Morphological Descriptions
**Pattern**: Detailed cellular and tissue descriptions
**Example**:
```
"Células atípicas en la capa basal que muestran pleomorfismo nuclear marcado con núcleos irregulares hipercromáticos y mitosis ocasionales compatible con carcinoma basocelular infiltrante"
```

#### 4. Immunohistochemistry Results
**Pattern**: Technical results with markers
**Example**:
```
"Inmunohistoquímica positiva para citoqueratinas y negativa para melanoma compatible con carcinoma escamocelular bien diferenciado"
```

### Medical Terminology Recognition

#### Dermatopathology
- **✅ "carcinoma basocelular"** (not "vasocelular")
- **✅ "pleomorfismo nuclear"** (not "empleomorfismo")
- **✅ "células atípicas"**
- **✅ "hiperqueratosis"**
- **✅ "dermis papilar"**
- **✅ "invasión focal"**

#### Gastroenterology
- **✅ "gastritis crónica moderada activa"**
- **✅ "metaplasia intestinal incompleta"**
- **✅ "helicobacter spp"**
- **✅ "clasificación de viena"**
- **✅ "olga estadio"**
- **✅ "olgim estadio"**

#### Cytopathology
- **✅ "células endocervicales"**
- **✅ "células exocervicales"**
- **✅ "tinción de papanicolau"**
- **✅ "atipias escamosas"**
- **✅ "asc us"**
- **✅ "virus papiloma humano"**

## ⚙️ Advanced Configuration

### Customizing Medical Dictionary

#### Adding New Terms
```bash
# Add single term
~/voice-bridge-claude/scripts/agregar_termino_medico.sh "carcinoma adenoescamoso" patologia_molecular

# Add complete phrase
~/voice-bridge-claude/scripts/agregar_termino_medico.sh "compatible con adenocarcinoma pulmonar" frases_completas
```

#### Bulk Term Addition
```bash
# Edit dictionary files directly
nano ~/voice-bridge-claude/config/diccionarios/patologia_molecular.txt

# Add your terms (one per line)
carcinoma neuroendocrino
tumor de células gigantes
sarcoma de partes blandas
```

### Audio Optimization

#### Microphone Settings
```bash
# Optimal microphone level (85% recommended)
pactl set-source-volume @DEFAULT_SOURCE@ 85%

# Noise suppression
pactl load-module module-echo-cancel

# Test audio quality
arecord -f cd -t wav -d 5 test.wav && aplay test.wav
```

#### TTS Voice Customization
```bash
# Edit configuration
nano ~/voice-bridge-claude/config/voice_bridge_config.ini

# Change TTS voice
tts_voice = es-CO-GonzaloNeural  # Male voice
tts_voice = es-CO-SalomeNeural   # Female voice (default)
```

### Claude Desktop Integration

#### Automatic Sending Configuration
1. **Enable auto-send**: Check "Envío automático a Claude" in GUI
2. **Verify Claude window**: Must be titled exactly "Claude"
3. **Test integration**: Dictate → Should appear in Claude automatically

#### Manual Sending
1. **Select text**: Highlight desired transcription
2. **Click "📤 Enviar a Claude"**: Or use hotkey
3. **Verify delivery**: Text appears in Claude chat

#### Troubleshooting Claude Integration
```bash
# Verify Claude Desktop window
wmctrl -l | grep Claude

# Should show: 0x[id] 0 [hostname] Claude

# Test window automation
xdotool search --name "Claude" windowactivate
```

## 📊 Session Management

### Monitoring Performance

#### Real-time Status
- **Partial text**: Blue text shows real-time recognition
- **Final transcriptions**: Black text with timestamps
- **Confidence levels**: Displayed in system log
- **Medical terms**: Highlighted in confirmations

#### Session Statistics
- **Transcription count**: Shown in header
- **Session duration**: Live timer
- **Success rate**: Monitor in system log
- **Medical terms used**: TTS confirmations

### Saving and Export

#### Automatic Saving
- **Auto-save**: Transcriptions saved on app close
- **Location**: `~/voice-bridge-claude/logs/`
- **Format**: `transcripciones_patologia_YYYYMMDD_HHMMSS.txt`

#### Manual Export
1. **Click "💾 Guardar"**: Save current session
2. **Select all text**: Ctrl+A in transcription area
3. **Copy**: Ctrl+C for external use
4. **Integration**: Direct to medical records systems

### Session Workflows

#### Morning Setup Routine
```bash
# 1. Start systems
./start_voice_bridge_gui.sh
# Start Claude Desktop
# Open Obsidian with templates

# 2. Verify status
✅ Azure connected
✅ Medical dictionaries loaded
✅ TTS enabled
✅ Claude integration active

# 3. Test basic functionality
[Ctrl+Shift+V] → "pleomorfismo nuclear" → [Ctrl+Shift+S]
# Should hear confirmations and see correct transcription
```

#### Case Documentation Workflow
```bash
# 1. Start new case
[Ctrl+Shift+V] "Nuevo caso biopsia de piel"

# 2. Dictate observations
"Observo hiperqueratosis con células atípicas..."

# 3. Review and edit
# Check transcription accuracy
# Verify medical terms

# 4. Process with Claude
# Auto-sent or manual send
# Claude processes with templates

# 5. Finalize documentation
# Review Claude's structured report
# Export to medical records
```

## 🎯 Best Practices

### Dictation Techniques

#### Optimal Speaking Patterns
- **Pace**: Natural speaking speed (not slow)
- **Clarity**: Clear articulation without exaggeration
- **Pauses**: Natural pauses at phrase boundaries
- **Volume**: Consistent volume level
- **Distance**: 6-12 inches from microphone

#### Medical Phrase Construction
```
✅ Good: "Células atípicas en la capa basal con pleomorfismo nuclear"
❌ Avoid: "Células... atípicas... en la... capa basal"

✅ Good: "Compatible con carcinoma basocelular infiltrante"
❌ Avoid: "Compatible... eh... con carcinoma... basocelular"
```

#### Complex Observation Patterns
```
Structure: [Location] + [Morphology] + [Assessment] + [Conclusion]

Example: "Fragmentos de mucosa gástrica [location] con moderado proceso inflamatorio linfoplasmocitario [morphology] sin evidencia de malignidad [assessment] compatible con gastritis crónica [conclusion]"
```

### Error Prevention

#### Common Transcription Errors
| Intended | Common Error | Prevention |
|----------|--------------|------------|
| pleomorfismo | empleomorfismo | Speak clearly, check dictionary |
| basocelular | vasocelular | Ensure term in dictionary |
| Claude | Cloud | Check pronunciation, dictionary priority |
| helicobacter | helicobácter | Verify accent placement |

#### Quality Assurance
1. **Review each transcription**: Check for medical accuracy
2. **Use TTS confirmations**: Listen for key terms
3. **Monitor confidence**: Low confidence may indicate errors
4. **Customize dictionary**: Add frequently used terms

### Workflow Optimization

#### Hands-Free Microscopy
- **Position microphone**: Optimal distance and angle
- **Use TTS confirmations**: Verify reception without looking
- **Learn voice commands**: Master status and control commands
- **Practice hotkeys**: Muscle memory for start/stop

#### Integration with Medical Records
- **Standardize terminology**: Use consistent medical vocabulary
- **Template integration**: Leverage Obsidian templates
- **Quality control**: Review Claude's structured output
- **Export workflow**: Efficient transfer to records systems

## 🔧 Troubleshooting Usage Issues

### Recognition Problems

#### Poor Medical Term Recognition
```bash
# Check dictionary loading
grep -c "^[^#]" ~/voice-bridge-claude/config/diccionarios/*.txt
# Should show: patologia_molecular.txt:69, frases_completas.txt:26

# Add missing terms
~/voice-bridge-claude/scripts/agregar_termino_medico.sh "missing_term" patologia_molecular

# Restart Voice Bridge to reload
```

#### Phrases Being Cut
```bash
# Check timeout settings in config
nano ~/voice-bridge-claude/config/voice_bridge_config.ini

# Verify medical_mode is enabled
medical_mode = true

# Check Azure configuration in logs
tail -f ~/voice-bridge-claude/logs/voice_bridge_*.log
```

### Audio Issues

#### No TTS Confirmations
1. **Check TTS enabled**: ✅ "Respuestas por voz (TTS)" in GUI
2. **Test system audio**: `speaker-test -t wav -c 2 -l 1`
3. **Verify Azure TTS**: Check logs for TTS errors
4. **Audio permissions**: Ensure user in audio group

#### Poor Recognition Quality
1. **Check microphone levels**: `pactl list sources short`
2. **Adjust input volume**: Use pavucontrol GUI
3. **Test microphone**: Record and playback test
4. **Environmental factors**: Reduce background noise

### Integration Issues

#### Claude Desktop Not Receiving
```bash
# Verify Claude window
wmctrl -l | grep Claude

# Test window automation tools
which xdotool wmctrl
sudo apt install xdotool wmctrl  # if missing

# Check Claude window title exactly matches "Claude"
```

#### Obsidian Integration Problems
1. **Verify MCP setup**: Check Claude-Obsidian connection
2. **Template availability**: Ensure medical templates exist
3. **Permissions**: Check Obsidian file permissions
4. **Path configuration**: Verify Obsidian vault path

## 📚 Advanced Features

### Voice Command Development

#### Creating Custom Commands
```python
# Add to voice_bridge_app.py in process_voice_commands()
elif "nuevo protocolo" in text_lower:
    self.create_new_protocol()
    self.speak_text("Nuevo protocolo creado")
```

#### Specialized Medical Workflows
- **Tumor staging**: Voice commands for TNM classification
- **Grading systems**: Automated Gleason, Nottingham scoring
- **Protocol selection**: Voice-activated protocol templates

### Integration Extensions

#### Medical Records Systems
- **HL7 FHIR**: Integration with standard medical records
- **LIMS**: Laboratory information management systems
- **PACS**: Picture archiving and communication systems

#### Research Applications
- **Data collection**: Voice-driven research data entry
- **Statistical analysis**: Integration with R/Python analysis
- **Publication support**: Automated manuscript generation

## 📈 Performance Optimization

### System Monitoring

#### Performance Metrics
- **Recognition latency**: Target <0.5 seconds
- **Medical accuracy**: Target >95% with dictionary
- **Session stability**: No crashes during long sessions
- **Memory usage**: Monitor RAM consumption

#### Optimization Techniques
```bash
# Disable unnecessary services
sudo systemctl disable [unnecessary_services]

# Optimize audio latency
export PULSE_LATENCY_MSEC=30

# Monitor system resources
htop  # Check CPU/RAM usage during dictation
```

### Dictionary Maintenance

#### Regular Updates
```bash
# Weekly dictionary review
# Add new terms from recent cases
# Remove obsolete terminology
# Validate pronunciation accuracy

# Example maintenance script
#!/bin/bash
echo "=== Dictionary Maintenance ==="
echo "Total terms: $(grep -c '^[^#]' ~/voice-bridge-claude/config/diccionarios/*.txt)"
echo "Add new terms as needed..."
```

---

## 🎯 Daily Usage Summary

### Essential Steps
1. **Start**: Click Voice Bridge icon or run script
2. **Verify**: Check status indicators (system ready, terms loaded)
3. **Begin**: Ctrl+Shift+V to start recognition
4. **Dictate**: Natural speech with medical terminology
5. **Confirm**: Listen to TTS confirmations
6. **Process**: Review transcriptions and Claude integration
7. **Stop**: Ctrl+Shift+S when finished
8. **Save**: Export to medical records as needed

### Success Indicators
- ✅ Medical terms recognized correctly
- ✅ Long phrases not cut
- ✅ TTS confirmations working
- ✅ Claude integration functional
- ✅ No recognition errors in logs

Voice Bridge is now ready for professional pathology use. The system provides hands-free dictation optimized for medical terminology, enabling efficient documentation while maintaining focus on microscopic analysis.

For technical issues, see [TROUBLESHOOTING.md](GitHub/Voice-Bridge-Pathology/TROUBLESHOOTING.md)