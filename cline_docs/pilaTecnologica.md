# Pila Tecnológica - Asistente de Ventas IA

## Arquitectura General

### 🏗️ Patrón Arquitectónico
**Serverless + Extension Híbrida**
- Frontend: Chrome Extension (Manifest v3)
- Backend: AWS Serverless completamente gestionado
- Comunicación: WebSocket en tiempo real
- Procesamiento: Event-driven architecture

## Frontend - Chrome Extension

### 📱 Core Extension Technologies
- **Manifest Version**: v3 (obligatorio para nuevas extensiones)
- **Language**: TypeScript + JavaScript ES2022
- **Build Tool**: Webpack 5 con configuración específica para extensiones
- **UI Framework**: Vanilla JavaScript + Web Components (sin frameworks pesados)
- **Styling**: CSS3 + CSS Variables para theming

#### Justificación de Decisiones Frontend
- **Manifest v3**: Requerido por Chrome, mejor seguridad y rendimiento
- **TypeScript**: Type safety crítico para APIs de Chrome y AWS
- **Vanilla JS**: Evita overhead de frameworks en ambiente restringido
- **Web Components**: Encapsulación natural para UI de extensión

### 🔌 Chrome Extension APIs
```javascript
// APIs principales utilizadas
- chrome.sidePanel     // Panel lateral principal
- chrome.scripting     // Content scripts inyección
- chrome.storage       // Persistencia local
- chrome.activeTab     // Acceso a tabs activos
- chrome.webRequest    // Intercepción de requests (opcional)
- MediaDevices API     // Captura de audio del navegador
```

### 🎨 UI Components Architecture
```
src/extension/
├── manifest.json           // Configuración Manifest v3
├── background/             // Service Worker
│   ├── service-worker.ts   // Gestión de conexiones AWS
│   └── aws-connection.ts   // WebSocket handler
├── content/                // Content Scripts
│   ├── audio-capture.ts    // Captura de audio de reuniones
│   └── meeting-detector.ts // Detección de plataformas de reuniones
├── sidepanel/              // Panel lateral principal
│   ├── sidepanel.html      // UI principal
│   ├── sidepanel.ts        // Lógica de interfaz
│   ├── components/         // Web Components
│   │   ├── insight-card.ts // Tarjetas de insights
│   │   ├── transcription.ts// Transcripción en vivo
│   │   └── search-results.ts// Resultados de búsqueda
│   └── styles/             // CSS modular
├── popup/                  // Popup de configuración
└── assets/                 // Iconos y recursos
```

## Backend - AWS Serverless

### ☁️ Core AWS Services
```yaml
Servicios Principales:
├── API Gateway WebSocket  # Comunicación tiempo real
├── AWS Lambda            # Procesamiento serverless
├── Amazon Bedrock        # Claude 3.5 Sonnet para análisis
├── Amazon Transcribe     # Speech-to-text en español
├── Amazon OpenSearch     # Búsqueda vectorial
├── Amazon S3             # Almacenamiento de documentos
├── Amazon EventBridge    # Event routing
├── AWS Systems Manager   # Configuración y secretos
└── CloudWatch           # Monitoreo y logs
```

### 🔧 Infrastructure as Code
- **Framework**: AWS CDK v2 (TypeScript)
- **Runtime**: Node.js 20.x (Lambda)
- **Package Manager**: npm con workspaces
- **Deployment**: CDK Deploy + GitHub Actions

#### Justificación de Decisiones Backend
- **AWS CDK**: Type safety, mejor que CloudFormation/Terraform para AWS
- **Node.js 20**: Mejor performance, soporte nativo ES modules
- **Serverless**: Cero mantenimiento, escalabilidad automática, pay-per-use

### 🚀 Lambda Functions Architecture
```
aws-backend/
├── cdk/                    // Infrastructure definitions
│   ├── lib/
│   │   ├── api-stack.ts    // API Gateway + Lambda
│   │   ├── ai-stack.ts     // Bedrock + Transcribe
│   │   └── search-stack.ts // OpenSearch + S3
├── src/
│   ├── websocket/          // WebSocket handlers
│   │   ├── connect.ts      // Connection management
│   │   ├── disconnect.ts   // Cleanup
│   │   └── message.ts      // Message processing
│   ├── transcription/      // Audio processing
│   │   ├── transcribe.ts   // Transcribe integration
│   │   └── audio-utils.ts  // Audio format handling
│   ├── ai-analysis/        // Bedrock integration
│   │   ├── claude.ts       // Claude API wrapper
│   │   ├── prompts.ts      // Prompt templates (español)
│   │   └── insights.ts     // Insight extraction
│   ├── vector-search/      // OpenSearch integration
│   │   ├── embeddings.ts   // Text embeddings
│   │   ├── search.ts       // Semantic search
│   │   └── indexing.ts     // Document indexing
│   └── shared/             // Utilidades compartidas
└── tests/                  // Unit + integration tests
```

## Integraciones de IA

### 🤖 Amazon Bedrock (Claude 3.5 Sonnet)
```typescript
// Configuración principal
Model: "anthropic.claude-3-5-sonnet-20241022-v2:0"
Region: "us-east-1" // Disponibilidad de Claude
Max Tokens: 4096
Temperature: 0.3 // Consistencia en respuestas
```

**Prompts Especializados**:
- Análisis de conversaciones de ventas
- Extracción de insights estructurados
- Generación de emails de seguimiento
- Búsqueda de documentos relevantes
- Detección de preguntas del prospecto

### 🎙️ Amazon Transcribe
```typescript
// Configuración específica
Language: "es-MX" // Español mexicano
MediaFormat: "webm" // Formato del navegador
SampleRate: 16000 // Óptimo para voz
EnablePartialResults: true // Transcripción en tiempo real
```

### 🔍 Amazon OpenSearch
```typescript
// Configuración de búsqueda vectorial
Engine: "OpenSearch 2.11"
InstanceType: "t3.small.search" // Desarrollo
NodeCount: 1 // Escalable a 3+ en producción
VectorDimensions: 1536 // Compatible con text-embedding-3-small
IndexStrategy: "Time-based rolling indices"
```

## Desarrollo y Despliegue

### 🛠️ Herramientas de Desarrollo
```json
{
  "package_manager": "npm",
  "bundler": "webpack",
  "testing": {
    "unit": "jest",
    "e2e": "playwright",
    "extension": "web-ext"
  },
  "linting": {
    "typescript": "eslint + @typescript-eslint",
    "formatting": "prettier"
  },
  "git_hooks": "husky + lint-staged"
}
```

### 📦 Build y Packaging
```bash
# Extension build
npm run build:extension    # Webpack bundle para Chrome Web Store
npm run dev:extension      # Hot reload para desarrollo
npm run package:extension  # .zip para Chrome Web Store

# AWS infrastructure
npm run deploy:dev         # Deploy a ambiente desarrollo
npm run deploy:prod        # Deploy a ambiente producción
npm run synth             # Generar CloudFormation templates
```

### 🔄 CI/CD Pipeline
```yaml
# GitHub Actions workflow
Triggers:
  - Push to main → Deploy to production
  - Push to develop → Deploy to staging
  - Pull request → Run tests + security scan

Jobs:
  1. Extension build + test
  2. AWS CDK synth + test
  3. Security scanning (Snyk)
  4. Deploy infrastructure
  5. Integration tests
  6. Notification (Slack/Discord)
```

## Localización y Internacionalización

### 🌐 Estrategia de Localización
- **Idioma Principal**: Español (México)
- **Idioma Secundario**: Inglés (términos técnicos)
- **Formato**: Chrome i18n API + JSON files

```
_locales/
├── es/                 // Español principal
│   └── messages.json   // Strings de UI
├── en/                 // Inglés fallback
│   └── messages.json   // English strings
└── es_MX/              // Específico México
    └── messages.json   // Localizaciones específicas
```

### 🎯 Terminología de Ventas
- Prompts de IA optimizados para español mexicano
- Terminología específica de ventas B2B
- Formatos de email profesionales en español
- Frases y expresiones comunes en reuniones de ventas

## Monitoreo y Observabilidad

### 📊 Métricas Clave
```typescript
// Métricas de rendimiento
- Latencia de transcripción (objetivo: < 1s)
- Tiempo de respuesta de IA (objetivo: < 2s)
- Precisión de búsqueda vectorial (objetivo: > 80%)
- Tasa de error en conexiones WebSocket (objetivo: < 1%)

// Métricas de negocio
- Insights generados por reunión
- Documentos encontrados por búsqueda
- Emails de seguimiento creados
- Tiempo activo de la extensión
```

### 🔍 Logging Strategy
```json
{
  "frontend": "chrome.runtime logging + local storage",
  "backend": "CloudWatch Logs con structured logging",
  "format": "JSON structured logs",
  "retention": "30 días desarrollo, 90 días producción",
  "alerting": "CloudWatch Alarms + SNS notifications"
}
```

## Seguridad y Compliance

### 🔐 Security Framework
```typescript
// Extension security
- Content Security Policy (CSP) estricto
- Permisos mínimos necesarios en manifest
- Validación de input en content scripts
- Sanitización de output en UI

// AWS security
- IAM roles con least privilege
- VPC endpoints para servicios privados
- Encryption at rest (S3, OpenSearch)
- Encryption in transit (TLS 1.3)
- API rate limiting y throttling
```

### 📋 Compliance Considerations
- **GDPR**: No almacenamiento persistente de audio
- **Privacy**: Procesamiento local de audio antes de envío
- **Data Residency**: Configuración multi-región disponible
- **Audit Trail**: CloudTrail habilitado para todas las operaciones

## Costos y Escalabilidad

### 💰 Modelo de Costos
```yaml
Desarrollo (< 100 reuniones/mes):
  - Lambda: $1-5/mes
  - Bedrock: $10-20/mes  
  - Transcribe: $5-10/mes
  - OpenSearch: $15-25/mes
  - Total estimado: $30-60/mes

Producción (1000+ reuniones/mes):
  - Lambda: $20-50/mes
  - Bedrock: $100-300/mes
  - Transcribe: $50-150/mes
  - OpenSearch: $100-200/mes
  - Total estimado: $270-700/mes
```

### 📈 Escalabilidad Targets
- **Usuarios Concurrentes**: 1000+ simultáneos
- **Reuniones Simultáneas**: 500+ en paralelo
- **Latencia Global**: < 2s en cualquier región
- **Disponibilidad**: 99.9% SLA objetivo

---

*Última actualización: 14 de junio, 2025*
*Stack version: Chrome Extension Manifest v3 + AWS CDK v2*
