# Visão Geral da Arquitetura

## Padrão Arquitetural

O Caki utiliza uma arquitetura baseada em **componentes modulares** com separação clara de responsabilidades:

- **Screens** - Telas e UI principal
- **Services** - Lógica de negócio e integrações externas
- **Models** - Estruturas de dados
- **Widgets** - Componentes reutilizáveis
- **Managers** - Gerenciadores de estado específicos

## Fluxo de Dados

```
User Action → Screen → Service/Manager → Model → State Update → UI Rebuild
```

## Princípios de Design

### 1. Separação de Responsabilidades
Cada módulo tem uma responsabilidade única e bem definida:
- **Screens**: Apenas UI e coordenação
- **Services**: Lógica de negócio e integrações
- **Managers**: Gerenciamento de estado específico

### 2. Singleton Services
Serviços críticos (Analytics, RevenueCat) são implementados como singletons para garantir uma única instância em todo o app.

### 3. State Management
O projeto utiliza `StatefulWidget` para gerenciamento de estado local, com managers especializados para lógicas complexas (ex: `WidgetManager`, `FilterManager`).

### 4. Composição sobre Herança
Componentes são construídos através de composição de widgets menores e reutilizáveis.

## Estrutura de Pastas

```
lib/
├── config/              # Configurações do app
├── design_system/       # Sistema de design
│   ├── components/      # Componentes reutilizáveis
│   └── tokens/          # Tokens de design (cores, fontes)
├── filters/            # Filtros de imagem
├── models/             # Modelos de dados
├── screens/            # Telas do app
│   ├── camera/         # Tela de câmera
│   ├── editor/         # Tela de edição
│   └── subscription/   # Telas de assinatura
├── services/           # Serviços e lógica de negócio
├── utils/              # Utilitários
└── widgets/            # Widgets customizados
```

## Inicialização do App

O app inicializa na seguinte ordem:

1. **WidgetsFlutterBinding** - Garante que o Flutter está inicializado
2. **SystemChrome** - Configura status bar
3. **Firebase** - Inicializa Firebase Core
4. **Firebase Messaging** - Registra handler de background
5. **RevenueCat** - Inicializa serviço de assinaturas
6. **Analytics** - Inicializa serviço de analytics
7. **MaterialApp** - Inicia o app com SplashScreen

## Comunicação entre Módulos

### Services → Screens
Serviços expõem streams e métodos públicos que as screens consomem.

### Screens → Services
Screens chamam métodos dos serviços diretamente através de instâncias singleton.

### Managers → Screens
Managers são criados dentro das screens e gerenciam estado específico daquela tela.

## Tratamento de Erros

- Erros críticos são logados mas não impedem o funcionamento do app
- Serviços têm fallbacks para continuar funcionando mesmo em caso de falha
- Mensagens de erro são exibidas ao usuário quando necessário

## Performance

- Lazy loading de imagens e dados
- Processamento de imagens em background
- Cache de dados quando apropriado
- Otimização de rebuilds com `const` widgets

