# Guias de Desenvolvimento

## Convenções de Código

### Nomenclatura

#### Classes
Use PascalCase:
```dart
class MyService {}
class WidgetManager {}
```

#### Variáveis e Métodos
Use camelCase:
```dart
String myVariable = 'value';
void myMethod() {}
```

#### Constantes
Use camelCase com `const`:
```dart
static const String apiKey = 'key';
static const int maxItems = 10;
```

#### Arquivos
Use snake_case:
```dart
my_service.dart
widget_manager.dart
```

### Estrutura de Arquivos

#### Imports
Organize imports na seguinte ordem:
1. Dart SDK
2. Flutter
3. Pacotes externos
4. Imports relativos do projeto

```dart
// Dart SDK
import 'dart:async';

// Flutter
import 'package:flutter/material.dart';

// Pacotes externos
import 'package:firebase_core/firebase_core.dart';

// Imports relativos
import '../models/workout_data.dart';
import 'editor_screen.dart';
```

### Documentação

#### Comentários de Classe
```dart
/// Serviço para gerenciar analytics e tracking de eventos
class AnalyticsService {
  // ...
}
```

#### Comentários de Método
```dart
/// Inicializa o serviço de analytics
Future<void> initialize() async {
  // ...
}
```

## Padrões de Arquitetura

### Singleton Pattern

Use para serviços globais:
```dart
class MyService {
  static final MyService _instance = MyService._internal();
  factory MyService() => _instance;
  MyService._internal();
}
```

### Factory Pattern

Use para criar instâncias de diferentes fontes:
```dart
class WorkoutData {
  factory WorkoutData.fromHealthData({...}) {
    // Criação a partir de dados do Health
  }
  
  factory WorkoutData.mock() {
    // Criação de dados mockados
  }
}
```

### Manager Pattern

Use para gerenciar estado complexo:
```dart
class WidgetManager {
  final List<WidgetInstance> _widgets = [];
  
  void addWidget(WidgetInstance widget) {
    _widgets.add(widget);
    _notifyListeners();
  }
  
  void removeWidget(String id) {
    _widgets.removeWhere((w) => w.id == id);
    _notifyListeners();
  }
}
```

## Gerenciamento de Estado

### Estado Local (setState)

Use para estado simples:
```dart
bool _isLoading = false;

void _toggleLoading() {
  setState(() {
    _isLoading = !_isLoading;
  });
}
```

### Managers para Estado Complexo

Use managers para lógica complexa:
```dart
late final WidgetManager _widgetManager;

@override
void initState() {
  super.initState();
  _widgetManager = WidgetManager();
}
```

## Tratamento de Erros

### Try-Catch

Sempre trate erros:
```dart
try {
  await service.initialize();
} catch (e, stackTrace) {
  debugPrint('❌ Erro: $e');
  debugPrint('❌ Stack trace: $stackTrace');
  // Não quebrar o app, continuar funcionando
}
```

### Erros Críticos vs Não-Críticos

**Erros Críticos**: Quebram funcionalidade essencial
```dart
try {
  await criticalService.initialize();
} catch (e) {
  // Exibir erro ao usuário
  showErrorDialog(context, 'Erro crítico: $e');
}
```

**Erros Não-Críticos**: Não impedem funcionamento
```dart
try {
  await optionalService.initialize();
} catch (e) {
  debugPrint('⚠️ Serviço opcional falhou: $e');
  // Continuar sem o serviço
}
```

## Performance

### Const Widgets

Use `const` quando possível:
```dart
const Text('Hello')
const SizedBox(height: 16)
```

### RepaintBoundary

Use para otimizar repaints:
```dart
RepaintBoundary(
  child: ExpensiveWidget(),
)
```

### Lazy Loading

Carregue dados sob demanda:
```dart
FutureBuilder<List<WorkoutData>>(
  future: _loadWorkouts(),
  builder: (context, snapshot) {
    // ...
  },
)
```

## Testes

### Testes Unitários

```dart
test('WorkoutData.fromHealthData', () {
  final workout = WorkoutData.fromHealthData(
    distanceMeters: 1000,
    duration: Duration(minutes: 10),
    // ...
  );
  
  expect(workout.distance, '1.0 km');
  expect(workout.movingTime, '0:10:00');
});
```

### Testes de Widget

```dart
testWidgets('MyWidget test', (WidgetTester tester) async {
  await tester.pumpWidget(
    MaterialApp(
      home: MyWidget(),
    ),
  );
  
  expect(find.text('Hello'), findsOneWidget);
  await tester.tap(find.byType(Button));
  await tester.pump();
  expect(find.text('Clicked'), findsOneWidget);
});
```

## Logging

### Debug Print

Use `debugPrint` para logs:
```dart
debugPrint('✅ Serviço inicializado');
debugPrint('⚠️ Aviso: algo aconteceu');
debugPrint('❌ Erro: $error');
```

### Emojis para Categorização

- ✅ Sucesso
- ⚠️ Aviso
- ❌ Erro
- 📊 Analytics
- 🔄 Atualização

## Analytics

### Registrar Eventos

Sempre registre eventos importantes:
```dart
AnalyticsService().logEvent('Button Clicked', parameters: {
  'Button Name': 'Save',
  'Screen': 'Editor',
});
```

### Screen Views

Registre visualizações de tela:
```dart
@override
void initState() {
  super.initState();
  AnalyticsService().logScreenView('EditorScreen');
}
```

## Acessibilidade

### Semantics

Use `Semantics` para screen readers:
```dart
Semantics(
  label: 'Botão de salvar',
  button: true,
  child: IconButton(
    icon: Icon(Icons.save),
    onPressed: () {},
  ),
)
```

### Tamanhos de Toque

Mínimo 44x44 pontos:
```dart
SizedBox(
  width: 44,
  height: 44,
  child: IconButton(...),
)
```

## Internacionalização

### Strings

Prepare para i18n:
```dart
// Por enquanto, use strings diretas
Text('Hello World')

// No futuro, use:
Text(AppLocalizations.of(context)!.helloWorld)
```

## Versionamento

### Versionamento Semântico

Siga [Semantic Versioning](https://semver.org/):
- **MAJOR**: Mudanças incompatíveis
- **MINOR**: Novas funcionalidades compatíveis
- **PATCH**: Correções de bugs

### Changelog

Mantenha um changelog:
```markdown
## [1.0.4] - 2024-01-01
### Added
- Novo filtro de imagem
- Widget de temperatura

### Fixed
- Bug na câmera
- Erro ao compartilhar
```

## Git Workflow

### Branches

- `main`: Código de produção
- `develop`: Desenvolvimento
- `feature/`: Novas funcionalidades
- `fix/`: Correções de bugs

### Commits

Use mensagens descritivas:
```bash
git commit -m "feat: adiciona novo filtro de imagem"
git commit -m "fix: corrige bug na câmera"
git commit -m "docs: atualiza documentação"
```

### Prefixos de Commit

- `feat:` Nova funcionalidade
- `fix:` Correção de bug
- `docs:` Documentação
- `style:` Formatação
- `refactor:` Refatoração
- `test:` Testes
- `chore:` Tarefas de manutenção

## Code Review

### Checklist

- [ ] Código segue convenções
- [ ] Testes passam
- [ ] Sem warnings
- [ ] Documentação atualizada
- [ ] Analytics implementado
- [ ] Tratamento de erros
- [ ] Performance otimizada

## Recursos

- [Effective Dart](https://dart.dev/guides/language/effective-dart)
- [Flutter Best Practices](https://flutter.dev/docs/development/ui/best-practices)
- [Material Design](https://material.io/design)

