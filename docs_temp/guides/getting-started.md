# Guia de Início Rápido

## Pré-requisitos

Antes de começar, certifique-se de ter instalado:

- **Flutter SDK 3.9+**
- **Dart 3.9+**
- **Android Studio** ou **Xcode** (para desenvolvimento)
- **Git**

## Instalação

### 1. Clonar o Repositório

```bash
git clone https://github.com/marquesedel/caki.git
cd caki
```

### 2. Instalar Dependências

```bash
flutter pub get
```

### 3. Configurar Plataformas

#### iOS
```bash
cd ios
pod install
cd ..
```

#### Android
As configurações já estão prontas. Certifique-se de ter o Android SDK instalado.

## Configuração

### Firebase

1. Adicione os arquivos de configuração:
   - **iOS**: `ios/Runner/GoogleService-Info.plist`
   - **Android**: `android/app/google-services.json`

2. Configure o Firebase no console:
   - Crie um projeto Firebase
   - Adicione apps iOS e Android
   - Baixe os arquivos de configuração

### RevenueCat

1. Crie uma conta no [RevenueCat](https://www.revenuecat.com/)
2. Configure o projeto:
   - API Key: `appl_OVNIKewaANxIhFiMFZyMpzIdPOS`
   - Entitlement: `Caki Pro`
   - Offering: `sale`
   - Products: `monthly`, `yearly`, `lifetime`

3. Configure produtos nas stores:
   - App Store Connect (iOS)
   - Google Play Console (Android)

### Mixpanel

1. Crie uma conta no [Mixpanel](https://mixpanel.com/)
2. Obtenha o token do projeto
3. Atualize o token em `lib/services/analytics_service.dart`:
```dart
static const String _mixpanelToken = 'SEU_TOKEN_AQUI';
```

## Executar o App

### Modo Debug

```bash
flutter run
```

### Modo Release

```bash
flutter run --release
```

### Plataforma Específica

```bash
# iOS
flutter run -d ios

# Android
flutter run -d android
```

## Estrutura do Projeto

```
lib/
├── config/              # Configurações
├── design_system/       # Sistema de design
├── filters/            # Filtros de imagem
├── models/             # Modelos de dados
├── screens/            # Telas
├── services/           # Serviços
├── utils/              # Utilitários
└── widgets/            # Widgets customizados
```

## Desenvolvimento

### Adicionar Nova Tela

1. Crie o arquivo em `lib/screens/`:
```dart
class MyScreen extends StatefulWidget {
  const MyScreen({super.key});
  
  @override
  State<MyScreen> createState() => _MyScreenState();
}

class _MyScreenState extends State<MyScreen> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('My Screen')),
      body: Center(child: Text('Hello World')),
    );
  }
}
```

2. Navegue para a tela:
```dart
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => MyScreen()),
);
```

### Adicionar Novo Serviço

1. Crie o arquivo em `lib/services/`:
```dart
class MyService {
  static final MyService _instance = MyService._internal();
  factory MyService() => _instance;
  MyService._internal();
  
  Future<void> initialize() async {
    // Inicialização
  }
}
```

2. Inicialize no `main.dart`:
```dart
await MyService().initialize();
```

### Adicionar Novo Widget

1. Crie o arquivo em `lib/widgets/`:
```dart
class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      // Seu widget
    );
  }
}
```

2. Use no app:
```dart
MyWidget()
```

## Debugging

### Logs

O app usa `debugPrint` para logs:
```dart
debugPrint('Mensagem de debug');
```

### Breakpoints

Use breakpoints no IDE para debugar:
- **Android Studio**: Clique na margem esquerda
- **VS Code**: Clique na margem esquerda

### Flutter Inspector

Use o Flutter Inspector para inspecionar widgets:
```bash
flutter run
# Abra Flutter Inspector no IDE
```

## Testes

### Executar Testes

```bash
flutter test
```

### Testes de Widget

```dart
testWidgets('MyWidget test', (WidgetTester tester) async {
  await tester.pumpWidget(MyWidget());
  expect(find.text('Hello'), findsOneWidget);
});
```

## Build

### Android APK

```bash
flutter build apk --release
```

### Android App Bundle

```bash
flutter build appbundle --release
```

### iOS

```bash
flutter build ios --release
```

## Troubleshooting

### Erro: "No devices found"

Certifique-se de ter um dispositivo conectado ou emulador rodando:
```bash
flutter devices
```

### Erro: "Pod install failed" (iOS)

Limpe e reinstale pods:
```bash
cd ios
rm -rf Pods Podfile.lock
pod install
cd ..
```

### Erro: "Gradle build failed" (Android)

Limpe o build:
```bash
cd android
./gradlew clean
cd ..
flutter clean
flutter pub get
```

## Próximos Passos

1. Leia a [Documentação de Arquitetura](../architecture/overview.md)
2. Explore o [Design System](../design-system/introduction.md)
3. Veja os [Guias de Desenvolvimento](./development.md)
4. Consulte a [API Reference](../api/overview.md)

## Recursos

- [Flutter Documentation](https://flutter.dev/docs)
- [Dart Documentation](https://dart.dev/guides)
- [RevenueCat Documentation](https://docs.revenuecat.com/)
- [Mixpanel Documentation](https://developer.mixpanel.com/docs)

