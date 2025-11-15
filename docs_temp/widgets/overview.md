# Sistema de Widgets

## Visão Geral

O sistema de widgets permite adicionar elementos visuais arrastáveis ao editor, como dados de treino, streaks e temperatura.

## Estrutura

```
widgets/
├── widgets_registry.dart        # Registro de widgets
├── workout_stats/              # Widgets de dados de treino
│   ├── minimal_design.dart
│   ├── sport_design.dart
│   ├── elegant_design.dart
│   ├── bold_design.dart
│   ├── gradient_design.dart
│   ├── compact_design.dart
│   ├── detailed_design.dart
│   ├── minimal_simple_design.dart
│   ├── minimal_top_design.dart
│   ├── vertical_bold_design.dart
│   └── custom_position_design.dart
├── streak/                     # Widgets de streak
│   └── streak_design.dart
└── temperature/               # Widgets de temperatura
    ├── temperature_simple_design.dart
    ├── temperature_bold_design.dart
    └── temperature_circle_design.dart
```

## Tipos de Widgets

### 1. Workout Stats
Widgets que exibem dados de treino (distância, tempo, elevação, ritmo, calorias).

#### Designs Disponíveis

**Minimal Design**
- Design minimalista e limpo
- Posição: bottom
- Estilo: minimal

**Sport Design**
- Design esportivo vibrante
- Posição: bottom
- Estilo: sport

**Elegant Design**
- Design elegante e sofisticado
- Posição: bottom
- Estilo: elegant

**Bold Design**
- Design em negrito com impacto visual
- Posição: bottom
- Estilo: bold

**Gradient Design**
- Design com gradiente de cores
- Posição: bottom
- Estilo: sport

**Compact Design**
- Design compacto com informações essenciais
- Posição: bottom
- Estilo: minimal

**Detailed Design**
- Design detalhado com todas as informações
- Posição: bottom
- Estilo: detailed

**Minimal Simple Design**
- Versão simplificada do minimal
- Posição: bottom
- Estilo: minimal

**Minimal Top Design**
- Design minimalista na parte superior
- Posição: top
- Estilo: minimal

**Vertical Bold Design**
- Design em negrito vertical
- Posição: center
- Estilo: bold

**Custom Position Design**
- Design com posição customizável
- Posição: custom
- Estilo: sport

### 2. Streak Widget
Widget que exibe sequência de treinos (streaks).

**Localização**: `lib/widgets/streak/streak_design.dart`

Exibe:
- Número de dias consecutivos
- Ícone de fogo
- Design animado

### 3. Temperature Widget
Widgets que exibem temperatura atual.

#### Designs Disponíveis

**Temperature Simple Design**
- Design simples com temperatura
- Posição: top-right
- Estilo: minimal

**Temperature Bold Design**
- Design em negrito com temperatura
- Posição: top-right
- Estilo: bold

**Temperature Circle Design**
- Design circular com temperatura
- Posição: top-right
- Estilo: sport

## WidgetsRegistry

**Localização**: `lib/widgets/widgets_registry.dart`

Registra todos os widgets disponíveis:

```dart
class WidgetsRegistry {
  // Lista de todos os widgets
  static List<FrameDesign> get allWidgets => [
    // Workout Stats
    MinimalDesign(),
    SportDesign(),
    ElegantDesign(),
    BoldDesign(),
    GradientDesign(),
    CompactDesign(),
    DetailedDesign(),
    MinimalSimpleDesign(),
    MinimalTopDesign(),
    VerticalBoldDesign(),
    CustomPositionDesign(),
    
    // Streak
    StreakDesign(),
    
    // Temperature
    TemperatureSimpleDesign(),
    TemperatureBoldDesign(),
    TemperatureCircleDesign(),
  ];
  
  // Obter widget por ID
  static FrameDesign? getWidgetById(String id) {
    return allWidgets.firstWhere(
      (widget) => widget.id == id,
      orElse: () => null,
    );
  }
}
```

## WidgetInstance

Cada widget adicionado ao editor é uma instância de `WidgetInstance`:

```dart
class WidgetInstance {
  final String id;              // ID único
  final FrameDesign design;     // Design do widget
  Offset position;              // Posição na tela
  double scale;                 // Escala (1.0 = normal)
  double rotation;               // Rotação em graus
  bool isDragging;              // Se está sendo arrastado
  bool isDeleting;              // Se está sendo deletado
  Size? renderedSize;           // Tamanho após renderização
}
```

## Adicionar Widgets

No editor, widgets são adicionados através do `WidgetManager`:

```dart
// Adicionar widget
void _addWidget(FrameDesign design) {
  final widget = WidgetInstance(
    id: 'widget_${DateTime.now().millisecondsSinceEpoch}',
    design: design,
    position: Offset(100, 200), // Posição inicial
    scale: 1.0,
    rotation: 0.0,
  );
  
  _widgetManager.addWidget(widget);
}
```

## Editar Widgets

Widgets podem ser editados através do `EditableWidgetManager`:

1. **Tocar no widget**: Ativa modo de edição
2. **Bottom sheet de edição**: Permite editar dados
3. **Atualização**: Widget é atualizado com novos dados

## Gestos

### Arrastar
- Toque e arraste para mover widget
- Snap para posições específicas
- Linhas de guia durante arraste

### Redimensionar
- Pinch para redimensionar
- Limites mínimo/máximo

### Deletar
- Arrastar para zona de deletar
- Feedback visual durante arraste

## Renderização

Widgets são renderizados usando `FramePreviewWidget`:

```dart
FramePreviewWidget(
  widgetInstance: widgetInstance,
  workoutData: workoutData,
  isDragging: isDragging,
  onTap: () => _editWidget(widgetInstance),
)
```

## Custom Frame Builder

Alguns widgets usam `customFrameBuilder` para renderização customizada:

```dart
FrameDesign(
  id: 'custom',
  name: 'Custom',
  customFrameBuilder: (isDragging, workoutData) {
    return CustomWidget(
      workoutData: workoutData,
      isDragging: isDragging,
    );
  },
)
```

## Dados do Widget

### WorkoutData
Widgets de workout stats recebem `WorkoutData`:
- Distância
- Tempo
- Elevação
- Ritmo
- Calorias
- Data
- Tipo de atividade
- Temperatura (opcional)

### Streak Data
Widgets de streak recebem dados de streak:
- Número de dias consecutivos
- Data do último treino

### Temperature Data
Widgets de temperatura recebem:
- Temperatura atual (String)
- Localização (opcional)

## Posicionamento

### Posições Padrão
- **Bottom**: Parte inferior da tela
- **Top**: Parte superior da tela
- **Center**: Centro da tela

### Posição Customizada
Alguns widgets permitem posição customizada:
- `customOffsetX`: Offset horizontal (-1.0 a 1.0)
- `customOffsetY`: Offset vertical (-1.0 a 1.0)
- `useCustomPosition`: Usar posição customizada

## Backgrounds Pré-configurados

Alguns widgets têm backgrounds pré-configurados:
- `hasPresetBackground`: Se tem background pré-configurado
- `presetBackgroundColors`: Lista de cores
- `presetBackgroundIsGradient`: Se é gradiente

## Boas Práticas

1. **IDs únicos**: Sempre use IDs únicos para widgets
2. **Posições iniciais**: Defina posições iniciais sensatas
3. **Escalas**: Mantenha escala padrão em 1.0
4. **Renderização**: Otimize renderização com `RepaintBoundary`
5. **Gestos**: Implemente feedback visual em gestos

## Criar Novo Widget

Para criar um novo widget:

1. **Criar classe do design**:
```dart
class MyCustomWidget extends FrameDesign {
  MyCustomWidget() : super(
    id: 'my_custom',
    name: 'My Custom',
    backgroundColor: Colors.black,
    textColor: Colors.white,
    position: FramePosition.bottom,
    style: FrameStyle.minimal,
  );
}
```

2. **Registrar no WidgetsRegistry**:
```dart
static List<FrameDesign> get allWidgets => [
  // ... outros widgets
  MyCustomWidget(),
];
```

3. **Implementar renderização** (se necessário):
```dart
customFrameBuilder: (isDragging, workoutData) {
  return MyCustomWidgetWidget(
    workoutData: workoutData,
    isDragging: isDragging,
  );
}
```

