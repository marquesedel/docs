# Arquitetura das Screens

## Visão Geral

As screens são organizadas por funcionalidade e seguem um padrão consistente de estruturação.

## Estrutura de uma Screen

```dart
class MyScreen extends StatefulWidget {
  // Props da screen
  final String param;
  
  const MyScreen({super.key, required this.param});
  
  @override
  State<MyScreen> createState() => _MyScreenState();
}

class _MyScreenState extends State<MyScreen> {
  // Managers e Services
  late final SomeManager _manager;
  
  // Estado local
  bool _isLoading = false;
  
  @override
  void initState() {
    super.initState();
    _manager = SomeManager();
    _initialize();
  }
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      // UI
    );
  }
}
```

## Screens Principais

### 1. SplashScreen
**Localização**: `lib/screens/splash_screen.dart`

**Responsabilidades**:
- Primeira tela exibida ao abrir o app
- Verifica onboarding e navega para tela apropriada
- Inicializa serviços necessários

**Fluxo**:
```
SplashScreen → OnboardingScreen (se necessário) → CameraScreen
```

### 2. OnboardingScreen
**Localização**: `lib/screens/onboarding_screen.dart`

**Responsabilidades**:
- Apresenta o app para novos usuários
- Múltiplas etapas com navegação
- Salva status de onboarding completo

**Eventos Analytics**:
- `Onboarding Started`
- `Onboarding Step Viewed`
- `Onboarding Completed`

### 3. CameraScreen
**Localização**: `lib/screens/camera/camera_screen.dart`

**Responsabilidades**:
- Captura de fotos usando câmera nativa
- Seleção de fotos da galeria
- Navegação para editor após captura

**Componentes**:
- `CameraTopBar` - Barra superior com controles
- `CameraBottomControls` - Controles inferiores
- `CameraSelector` - Seletor de câmera (frontal/traseira)
- `GalleryButton` - Botão para acessar galeria
- `FocusIndicator` - Indicador de foco

**Managers**:
- `ZoomManager` - Gerencia zoom da câmera

**Eventos Analytics**:
- `Camera Opened`
- `Photo Taken`
- `Photo From Gallery`
- `Editor Opened`

### 4. EditorScreen
**Localização**: `lib/screens/editor/editor_screen.dart`

**Responsabilidades**:
- Edição completa de fotos
- Aplicação de filtros
- Adição e edição de widgets
- Configuração de backgrounds
- Captura e compartilhamento

**Estrutura Interna**:
```
editor/
├── editor_screen.dart          # Tela principal
├── bars/                       # Barras de UI
│   ├── topbar/                 # Barra superior
│   └── bottombar/              # Barra inferior
├── components/                 # Componentes de UI
│   ├── image/                 # Componentes de imagem
│   ├── overlay/               # Overlays
│   └── ui/                    # Componentes UI gerais
├── managers/                   # Gerenciadores de estado
├── services/                   # Serviços do editor
├── gestures/                   # Handlers de gestos
├── dialogs/                    # Diálogos e bottom sheets
└── utils/                      # Utilitários
```

**Managers**:
- `WidgetManager` - Gerencia widgets adicionados
- `FilterManager` - Gerencia filtros aplicados
- `EditableWidgetManager` - Gerencia edição de widgets
- `ImageEditorState` - Estado de edição de imagem
- `DataLoader` - Carrega dados de treino e temperatura

**Eventos Analytics**:
- `Filter Applied`
- `Widget Added`
- `Widget Removed`
- `Background Changed`
- `Stroke Toggled`
- `Widget Edited`
- `Photo Shared`

### 5. PaywallScreen
**Localização**: `lib/screens/subscription/paywall_screen.dart`

**Responsabilidades**:
- Exibe paywall do RevenueCat
- Gerencia compras e assinaturas
- Restaura compras anteriores

**Eventos Analytics**:
- `Paywall Viewed`
- `Purchase Started`
- `Purchase Completed`
- `Purchase Cancelled`

## Padrões de Navegação

### Navegação com Navigator
```dart
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => NextScreen()),
);
```

### Navegação com Dados
```dart
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => EditorScreen(
      imagePath: path,
      workoutData: data,
    ),
  ),
);
```

## Gerenciamento de Estado

### Estado Local
Para estado simples, use `setState()`:
```dart
bool _isLoading = false;

void _toggleLoading() {
  setState(() {
    _isLoading = !_isLoading;
  });
}
```

### Managers para Estado Complexo
Para lógica complexa, use managers:
```dart
late final WidgetManager _widgetManager;

@override
void initState() {
  super.initState();
  _widgetManager = WidgetManager();
}
```

## Lifecycle das Screens

1. **initState()** - Inicialização
2. **build()** - Construção da UI
3. **dispose()** - Limpeza de recursos

Sempre limpe recursos em `dispose()`:
```dart
@override
void dispose() {
  _controller.dispose();
  _manager.dispose();
  super.dispose();
}
```

