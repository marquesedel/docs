# Design System

## Visão Geral

O Design System do Caki fornece componentes reutilizáveis, tokens de design e padrões visuais consistentes em todo o app.

## Estrutura

```
design_system/
├── components/          # Componentes reutilizáveis
│   ├── buttons/        # Botões
│   ├── cards.dart      # Cards
│   ├── checkbox.dart   # Checkbox
│   ├── chip.dart       # Chip
│   └── switch.dart     # Switch
├── tokens/             # Tokens de design
│   ├── app_colors.dart # Cores
│   └── app_fonts.dart  # Fontes
└── design_system_screen.dart # Tela de demonstração
```

## Tokens de Design

### Cores
**Localização**: `lib/design_system/tokens/app_colors.dart`

O app usa uma paleta de cores consistente:

#### Cores Primárias
- **Primary**: `#FF5383` (Rosa vibrante)
- **Secondary**: `#e6ebee` (Rosa suave)

#### Cores de Background
- **Background**: `#000000` (Preto)
- **Background Secondary**: `#1C1C1E` (Cinza escuro)
- **Background Splash**: `#13141D` (Azul escuro)
- **Card Background**: `#121212` (Preto suave)

#### Cores de Texto
- **Text Primary**: `#FFFFFF` (Branco)
- **Text Secondary**: `#BDBDBD` (Cinza claro)
- **Text Tertiary**: `#757575` (Cinza médio)

#### Cores de Status
- **Success**: `#4CAF50` (Verde)
- **Error**: `#F44336` (Vermelho)
- **Warning**: `#FF9800` (Laranja)
- **Info**: `#2196F3` (Azul)

**Uso**:
```dart
import 'package:photosport/design_system/tokens/app_colors.dart';

Container(
  color: AppColors.primary,
  child: Text(
    'Texto',
    style: TextStyle(color: AppColors.textPrimary),
  ),
)
```

### Fontes
**Localização**: `lib/design_system/tokens/app_fonts.dart`

O app usa a fonte **Switzer** com múltiplos pesos:
- Regular (400)
- Medium (500)
- Semibold (600)
- Bold (700)
- Extrabold (800)

**Configuração no pubspec.yaml**:
```yaml
fonts:
  - family: Switzer
    fonts:
      - asset: fonts/Switzer-Regular.otf
        weight: 400
      - asset: fonts/Switzer-Medium.otf
        weight: 500
      # ... outros pesos
```

## Componentes

### Botões

**Localização**: `lib/design_system/components/buttons/`

#### PrimaryButton
Botão principal com cor rosa.

```dart
DesignSystemButtons.primaryButton(
  text: 'Salvar',
  onPressed: () {},
)
```

#### SecondaryButton
Botão secundário com cor rosa suave.

```dart
DesignSystemButtons.secondaryButton(
  text: 'Cancelar',
  onPressed: () {},
)
```

#### OutlineButton
Botão com borda rosa e fundo transparente.

```dart
DesignSystemButtons.outlineButton(
  text: 'Ver Mais',
  onPressed: () {},
)
```

#### TextButton
Botão de texto com cor rosa.

```dart
DesignSystemButtons.textButton(
  text: 'Esqueci minha senha',
  onPressed: () {},
)
```

#### ControlButton
Botão circular com blur (usado na câmera).

```dart
DesignSystemButtons.controlButton(
  icon: Icons.settings,
  onTap: () {},
)
```

#### GalleryButton
Botão da galeria com preview de imagem.

```dart
DesignSystemButtons.galleryButton(
  imagePath: '/path/to/image',
  onTap: () {},
)
```

### Cards

**Localização**: `lib/design_system/components/cards.dart`

#### StandardCard
Card padrão com background escuro.

```dart
DesignSystemCards.standardCard(
  child: Text('Conteúdo'),
)
```

#### IntegrationCard
Card para integrações (usado nas settings).

```dart
DesignSystemCards.integrationCard(
  title: 'Health',
  icon: Icons.favorite,
  onTap: () {},
)
```

#### InfoCard
Card para informações (usado nas settings).

```dart
DesignSystemCards.infoCard(
  title: 'Versão',
  value: '1.0.4',
)
```

### Outros Componentes

#### Checkbox
**Localização**: `lib/design_system/components/checkbox.dart`

```dart
DesignSystemCheckbox(
  value: _checked,
  onChanged: (value) => setState(() => _checked = value),
)
```

#### Chip
**Localização**: `lib/design_system/components/chip.dart`

```dart
DesignSystemChip(
  label: 'Tag',
  onDeleted: () {},
)
```

#### Switch
**Localização**: `lib/design_system/components/switch.dart`

```dart
DesignSystemSwitch(
  value: _enabled,
  onChanged: (value) => setState(() => _enabled = value),
)
```

## Padrões de Uso

### Espaçamento
- Padding padrão: `16.0`
- Border radius padrão: `12.0` (cards), `16.0` (botões especiais)

### Tema
O app usa Material 3 com tema escuro:
```dart
ThemeData(
  colorScheme: ColorScheme.fromSeed(
    seedColor: AppColors.primary,
    brightness: Brightness.dark,
  ),
  useMaterial3: true,
)
```

## Tela de Demonstração

**Localização**: `lib/design_system/design_system_screen.dart`

A tela de demonstração mostra todos os componentes disponíveis. Acesse através da tela de dev pages.

