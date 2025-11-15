# Dependências do Projeto

## Visão Geral

Este documento lista todas as dependências do projeto Caki, suas versões e propósitos.

## Dependências Principais

### Flutter e Dart
- **flutter**: SDK Flutter (3.9+)
- **cupertino_icons**: Ícones do iOS (^1.0.8)

### Câmera e Imagens
- **camera**: Captura de fotos nativa (^0.11.0+2)
- **image_picker**: Seleção de imagens da galeria (^1.1.2)
- **photo_manager**: Gerenciamento de fotos (^3.3.0)
- **flutter_svg**: Renderização de SVGs (^2.0.10+1)

### Armazenamento e Arquivos
- **path_provider**: Acesso a diretórios do sistema (^2.1.4)
- **path**: Manipulação de caminhos (^1.9.0)
- **shared_preferences**: Armazenamento de preferências (^2.3.2)

### Compartilhamento e URLs
- **share_plus**: Compartilhamento nativo (^10.1.2)
- **url_launcher**: Abertura de URLs (^6.3.1)

### Permissões
- **permission_handler**: Gerenciamento de permissões (^11.3.1)

### Firebase
- **firebase_core**: Core do Firebase (^3.6.0)
- **firebase_messaging**: Notificações push (^15.1.3)
- **flutter_local_notifications**: Notificações locais (^18.0.1)

### Localização
- **geolocator**: Obter localização (^13.0.1)

### HTTP
- **http**: Requisições HTTP (^1.2.2)

### Internacionalização
- **intl**: Formatação de datas e números (^0.19.0)

### Assinaturas
- **purchases_flutter**: SDK do RevenueCat (^8.4.0)
- **purchases_ui_flutter**: UI do RevenueCat (^8.4.0)

### Analytics
- **mixpanel_flutter**: SDK do Mixpanel (^2.3.0)

## Dependências de Desenvolvimento

### Testes
- **flutter_test**: Framework de testes do Flutter

### Linting
- **flutter_lints**: Lints recomendados (^5.0.0)

### Splash Screen
- **flutter_native_splash**: Geração de splash screen nativa (^2.4.1)

## Configuração no pubspec.yaml

```yaml
dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.8
  camera: ^0.11.0+2
  path_provider: ^2.1.4
  path: ^1.9.0
  share_plus: ^10.1.2
  url_launcher: ^6.3.1
  permission_handler: ^11.3.1
  intl: ^0.19.0
  image_picker: ^1.1.2
  photo_manager: ^3.3.0
  firebase_core: ^3.6.0
  firebase_messaging: ^15.1.3
  flutter_local_notifications: ^18.0.1
  flutter_svg: ^2.0.10+1
  geolocator: ^13.0.1
  http: ^1.2.2
  shared_preferences: ^2.3.2
  purchases_flutter: ^8.4.0
  purchases_ui_flutter: ^8.4.0
  mixpanel_flutter: ^2.3.0

dev_dependencies:
  flutter_test:
    sdk: flutter
  flutter_lints: ^5.0.0
  flutter_native_splash: ^2.4.1
```

## Atualização de Dependências

### Verificar Versões Disponíveis

```bash
flutter pub outdated
```

### Atualizar Dependências

```bash
flutter pub upgrade
```

### Atualizar Major Versions

```bash
flutter pub upgrade --major-versions
```

## Gerenciamento de Versões

### Versionamento Semântico

As dependências usam versionamento semântico:
- `^1.2.3` - Permite atualizações de patch e minor
- `1.2.3` - Versão exata
- `>=1.2.3 <2.0.0` - Range específico

### Resolução de Conflitos

Se houver conflitos de versão:

1. Verifique as versões compatíveis:
```bash
flutter pub deps
```

2. Atualize manualmente no `pubspec.yaml`

3. Execute:
```bash
flutter pub get
```

## Dependências Nativas

### iOS (CocoaPods)

As dependências nativas do iOS são gerenciadas via CocoaPods:

```bash
cd ios
pod install
```

**Principais Pods**:
- Firebase
- RevenueCat
- Mixpanel
- Camera

### Android (Gradle)

As dependências nativas do Android são gerenciadas via Gradle:

```gradle
dependencies {
    implementation 'com.google.firebase:firebase-core'
    implementation 'com.revenuecat.purchases:purchases'
    // ...
}
```

## Configurações Específicas

### Firebase

**iOS**: `ios/Runner/GoogleService-Info.plist`
**Android**: `android/app/google-services.json`

### RevenueCat

**API Key**: Configurada em `lib/services/revenue_cat_service.dart`
**Entitlements**: Configurados no dashboard do RevenueCat

### Mixpanel

**Token**: Configurado em `lib/services/analytics_service.dart`

## Troubleshooting

### Erro: "Package not found"

```bash
flutter pub get
flutter clean
flutter pub get
```

### Erro: "Version conflict"

Atualize as versões no `pubspec.yaml` para versões compatíveis.

### Erro: "Pod install failed" (iOS)

```bash
cd ios
rm -rf Pods Podfile.lock
pod install
```

### Erro: "Gradle sync failed" (Android)

```bash
cd android
./gradlew clean
cd ..
flutter clean
flutter pub get
```

## Recursos

- [pub.dev](https://pub.dev/) - Repositório de pacotes Dart
- [Flutter Packages](https://pub.dev/flutter/packages) - Pacotes Flutter
- [Dependency Injection](https://pub.dev/packages/get_it) - Para injeção de dependências (futuro)

