# Tela de Editor

## Visão Geral

A `EditorScreen` é o coração do app, permitindo edição completa de fotos com filtros, widgets, backgrounds e muito mais.

**Localização**: `lib/screens/editor/editor_screen.dart`

## Funcionalidades Principais

- Aplicação de filtros de imagem
- Adição e edição de widgets (dados de treino)
- Configuração de backgrounds (gradientes e cores sólidas)
- Ajustes de imagem (exposição, contraste, saturação, etc.)
- Captura e compartilhamento da foto final
- Sistema de gestos (arrastar, redimensionar, rotacionar widgets)

## Estrutura de Pastas

```
editor/
├── editor_screen.dart              # Tela principal
├── bars/                          # Barras de UI
│   ├── topbar/
│   │   └── editor_top_bar.dart    # Barra superior
│   └── bottombar/                 # Barra inferior
│       ├── editor_bottom_bar.dart
│       └── menus/                 # Menus do bottom bar
├── components/                    # Componentes de UI
│   ├── image/                    # Componentes de imagem
│   │   ├── editable_image_widget.dart
│   │   ├── filtered_image_widget.dart
│   │   └── frame_preview_widget.dart
│   ├── overlay/                  # Overlays
│   │   ├── filter_name_overlay.dart
│   │   ├── processing_overlay.dart
│   │   └── delete_zone.dart
│   ├── widgets/                  # Widgets arrastáveis
│   │   └── draggable_widget_instance.dart
│   └── ui/                       # Componentes UI gerais
│       ├── editor_capture_area.dart
│       └── editor_vertical_slider.dart
├── managers/                     # Gerenciadores de estado
│   ├── filter_manager.dart
│   ├── widget_manager.dart
│   ├── editable_widget_manager.dart
│   └── data_loader.dart
├── services/                     # Serviços do editor
│   ├── capture_service.dart
│   └── image_processor.dart
├── gestures/                     # Handlers de gestos
│   ├── gesture_handler.dart
│   ├── widget_gesture_handler.dart
│   ├── snap_helper.dart
│   └── snap_guide_lines.dart
├── dialogs/                      # Diálogos e bottom sheets
│   ├── filter_code_dialog.dart
│   ├── workout_selector_bottom_sheet.dart
│   ├── widgets_selection_bottom_sheet.dart
│   ├── editable_widgets_selector_bottom_sheet.dart
│   └── streak_editor_bottom_sheet.dart
├── background/                   # Configurações de background
│   ├── background_helper.dart
│   └── background_options.dart
├── state/                        # Estados e modelos de estado
│   ├── image_editor_state.dart
│   └── frame_state.dart
└── utils/                        # Utilitários
    └── filter_code_generator.dart
```

## Managers

### WidgetManager
Gerencia widgets adicionados ao editor:
- Lista de `WidgetInstance`
- Adição/remoção de widgets
- Estado de arraste
- Dados de treino associados

### FilterManager
Gerencia filtros aplicados:
- Filtro atual selecionado
- Índice do filtro
- Aplicação de filtros

### EditableWidgetManager
Gerencia edição de widgets:
- Widget sendo editado
- Modo de edição
- Valores editáveis

### ImageEditorState
Gerencia estado de edição de imagem:
- Exposição, contraste, saturação
- Temperatura, tint, shadows, highlights
- Opção de edição selecionada

### DataLoader
Carrega dados externos:
- Dados de treino do Health Service
- Temperatura do Weather Service
- Estados de carregamento

## Componentes Principais

### EditorTopBar
Barra superior com:
- Botão de fechar
- Toggle de background
- Toggle de stroke (borda)
- Botão de compartilhar/publicar

### EditorBottomBar
Barra inferior com:
- Carrossel de designs (frames)
- Seletor de cores/gradientes para background
- Oculto durante arraste de widgets

### FilteredImageWidget
Widget que exibe a imagem com filtros aplicados.

### FramePreviewWidget
Widget do frame arrastável com dados do treino.

### DeleteZone
Zona de deletar widgets (aparece quando arrasta widget para cima).

## Filtros

O editor suporta múltiplos filtros de imagem:
- None (sem filtro)
- Black & White
- Cool
- Warm
- Film Airy
- Flower
- Friends
- Moody Orange City
- Napoli
- Sunny Landscape

Veja mais em [Filtros](./filters.md).

## Widgets

O editor permite adicionar widgets de dados de treino:
- Workout Stats (dados do treino)
- Streak (sequência de treinos)
- Temperature (temperatura atual)

Veja mais em [Widgets](./widgets.md).

## Backgrounds

O editor permite configurar backgrounds:
- Gradientes pré-configurados
- Cores sólidas
- Sem background (transparente)

## Gestos

### Arrastar Widgets
- Toque e arraste para mover widgets
- Snap para posições específicas
- Linhas de guia durante arraste

### Redimensionar
- Pinch para redimensionar widgets
- Limites mínimo/máximo

### Rotacionar
- Gestos de rotação (futuro)

### Deletar
- Arrastar widget para zona de deletar
- Feedback visual durante arraste

## Ajustes de Imagem

O editor permite ajustar:
- **Exposição**: Brilho geral da imagem
- **Contraste**: Diferença entre claro e escuro
- **Saturação**: Intensidade das cores
- **Temperatura**: Calor/frio da imagem
- **Tint**: Matiz da imagem
- **Shadows**: Sombras
- **Highlights**: Destaques
- **Curves**: Curvas de cor

## Captura e Compartilhamento

### CaptureService
**Localização**: `lib/screens/editor/services/capture_service.dart`

Captura a tela como imagem PNG em alta qualidade e abre o compartilhador nativo.

**Métodos**:
```dart
// Capturar e compartilhar
Future<void> captureAndShare(GlobalKey captureKey);
```

## Processamento de Imagem

### ImageProcessor
**Localização**: `lib/screens/editor/services/image_processor.dart`

Processa imagens:
- Flip horizontal (espelhar)
- Aplicação de filtros
- Ajustes de cor

**Métodos**:
```dart
// Espelhar imagem horizontalmente
Future<File> flipImageHorizontally(String imagePath);
```

## Eventos Analytics

A tela registra os seguintes eventos:

- **Filter Applied**: Quando um filtro é aplicado
  - Propriedades: `Filter Name`
- **Widget Added**: Quando um widget é adicionado
  - Propriedades: `Widget Type`
- **Widget Removed**: Quando um widget é removido
  - Propriedades: `Widget Type`
- **Background Changed**: Quando o background é alterado
  - Propriedades: `Background Type`, `Background Index`
- **Stroke Toggled**: Quando o stroke é ativado/desativado
  - Propriedades: `Stroke Enabled`
- **Widget Edited**: Quando um widget é editado
  - Propriedades: `Widget Type`
- **Photo Shared**: Quando uma foto é compartilhada
  - Propriedades: `Share Method`, `Has Filter`, `Filter Name`, `Has Widgets`, `Widget Count`, `Widget Types`, `Has Background`, `Background Type`

## Fluxo de Uso

1. **Abertura do Editor**
   ```
   CameraScreen captura foto → EditorScreen(imagePath)
   ```

2. **Aplicação de Filtro**
   ```
   User desliza horizontalmente → FilterManager aplica filtro → 
   FilteredImageWidget atualiza
   ```

3. **Adição de Widget**
   ```
   User toca botão de adicionar → BottomSheet de seleção → 
   WidgetManager adiciona widget → FramePreviewWidget renderiza
   ```

4. **Edição de Widget**
   ```
   User toca widget → EditableWidgetManager ativa edição → 
   BottomSheet de edição → WidgetManager atualiza
   ```

5. **Compartilhamento**
   ```
   User toca botão de compartilhar → CaptureService captura tela → 
   Share sheet nativo → Analytics registra evento
   ```

## Tratamento de Erros

- **Erro ao processar imagem**: Exibe overlay de erro
- **Erro ao carregar dados**: Continua sem dados
- **Erro ao capturar**: Exibe mensagem de erro
- **Erro ao compartilhar**: Exibe snackbar com erro

## Performance

- Processamento de imagens em background
- Lazy loading de widgets
- Cache de imagens processadas
- Otimização de rebuilds

## Melhorias Futuras

- [ ] Histórico de edições (undo/redo)
- [ ] Templates pré-configurados
- [ ] Export em diferentes formatos
- [ ] Filtros customizados pelo usuário
- [ ] Mais ajustes de imagem
- [ ] Suporte para múltiplas imagens

