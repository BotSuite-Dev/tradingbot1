# Robô de Trading Conservador para Índices de Mercado

## Visão Geral

Este projeto implementa um sistema automatizado de trading conservador especificamente projetado para operar no mercado de índices. O robô combina análise técnica avançada com monitoramento de notícias em tempo real para tomar decisões de investimento fundamentadas e minimizar riscos.

## Características Principais

### 🎯 Abordagem Conservadora
- Estratégia de baixo risco focada na preservação de capital
- Múltiplos indicadores técnicos para confirmação de sinais
- Sistema de tomada de decisão que prioriza a cautela sobre a agressividade
- Integração de análise fundamental através do sentimento de notícias

### 📊 Análise Técnica Automatizada
- **Médias Móveis**: SMA 20, 50 e 200 períodos
- **Bandas de Bollinger**: Identificação de sobrecompra/sobrevenda
- **RSI (Relative Strength Index)**: Análise de momentum
- **MACD**: Convergência e divergência de médias móveis

### 📰 Monitoramento de Notícias
- Análise de sentimento em tempo real
- Integração com APIs de notícias financeiras
- Classificação automática: positivo, negativo, neutro
- Influência nas decisões de trading

### 🖥️ Interface Web Intuitiva
- Dashboard em tempo real
- Visualização de indicadores técnicos
- Gráficos de preços interativos
- Sistema de alertas e notificações

## Arquitetura do Sistema

### Backend (Flask)
- API RESTful para análise técnica
- Endpoints para monitoramento de notícias
- Sistema de simulação de trading
- Integração com fontes de dados financeiros

### Frontend (HTML/CSS/JavaScript)
- Interface responsiva e moderna
- Visualização em tempo real dos dados
- Controles interativos para simulação
- Dashboard com métricas principais

### Componentes Principais
1. **technical_analysis.py**: Cálculo de indicadores técnicos
2. **news_monitor.py**: Monitoramento e análise de sentimento
3. **decision_maker.py**: Lógica de tomada de decisão
4. **trading.py**: Rotas da API Flask
5. **index.html**: Interface do usuário

## Instalação e Configuração

### Pré-requisitos
- Python 3.11+
- pip (gerenciador de pacotes Python)
- Chave da API News API (opcional, para notícias reais)

### Passos de Instalação

1. **Clone ou baixe o projeto**
```bash
cd trading_robot_app
```

2. **Ative o ambiente virtual**
```bash
source venv/bin/activate
```

3. **Instale as dependências**
```bash
pip install -r requirements.txt
```

4. **Configure a chave da API de notícias (opcional)**
```bash
export NEWS_API_KEY="sua_chave_aqui"
```

5. **Execute a aplicação**
```bash
python src/main.py
```

6. **Acesse a interface**
Abra o navegador em: http://localhost:5000

## Uso do Sistema

### Interface Principal
A interface principal apresenta três cards principais:

1. **Status do Sistema**: Mostra se o robô está ativo e funcionando
2. **Dados de Mercado**: Exibe preço atual, indicadores técnicos e sentimento
3. **Decisão de Trading**: Apresenta a recomendação atual (COMPRAR/VENDER/MANTER)

### Funcionalidades Disponíveis

#### Simulação de Trading
- Clique em "Simular Análise" para gerar dados simulados
- O sistema calculará automaticamente todos os indicadores
- Uma decisão de trading será apresentada com base na análise

#### Verificação de Status
- Clique em "Status do Sistema" para verificar a conectividade
- Mostra informações sobre versão e funcionalidades ativas

#### Visualização de Dados
- Gráfico de preços dos últimos 30 períodos
- Indicadores técnicos em tempo real
- Análise de sentimento das notícias

## API Endpoints

### GET /api/trading/status
Retorna o status atual do sistema.

**Resposta:**
```json
{
  "status": "active",
  "version": "1.0.0",
  "features": ["Análise Técnica", "Monitoramento de Notícias", ...],
  "timestamp": "2025-07-02T09:37:15"
}
```

### GET /api/trading/simulate
Executa uma simulação completa de trading.

**Resposta:**
```json
{
  "prices": [100.0, 101.5, ...],
  "current_price": 157.50,
  "sma_20": 155.25,
  "rsi": 65.5,
  "news_sentiment": "positive",
  "decision": "BUY",
  "timestamp": "2025-07-02T09:37:15"
}
```

### POST /api/trading/analysis
Analisa um conjunto de preços fornecido.

**Requisição:**
```json
{
  "prices": [100.0, 101.5, 102.0, ...]
}
```

### POST /api/trading/sentiment
Analisa o sentimento de um texto.

**Requisição:**
```json
{
  "text": "Mercado em alta com boas perspectivas"
}
```

### POST /api/trading/decision
Obtém uma decisão de trading baseada em preços e sentimento.

**Requisição:**
```json
{
  "prices": [100.0, 101.5, ...],
  "news_sentiment": "positive"
}
```

## Estratégia de Trading

### Filosofia Conservadora
O robô foi projetado com uma abordagem conservadora que prioriza:

1. **Preservação de Capital**: Evitar perdas significativas
2. **Confirmação Múltipla**: Requer vários sinais antes de agir
3. **Gestão de Risco**: Considera o sentimento de mercado
4. **Paciência**: Prefere MANTER quando há incerteza

### Lógica de Decisão

#### Sinais de Compra
- SMA 20 > SMA 50 e preço > SMA 20
- Preço próximo à banda inferior de Bollinger + RSI < 30
- RSI < 30 (sobrevenda)
- MACD > Linha de Sinal

#### Sinais de Venda
- SMA 20 < SMA 50 e preço < SMA 20
- Preço próximo à banda superior de Bollinger + RSI > 70
- RSI > 70 (sobrecompra)
- MACD < Linha de Sinal

#### Influência do Sentimento
- **Notícias Positivas**: Reforçam sinais de compra, anulam sinais de venda
- **Notícias Negativas**: Reforçam sinais de venda, anulam sinais de compra
- **Notícias Neutras**: Requerem mais confirmação técnica

#### Regra de Ouro
Em caso de sinais conflitantes ou incerteza, o sistema sempre escolhe MANTER.

## Dependências

### Principais Bibliotecas
- **Flask**: Framework web para API
- **Flask-CORS**: Suporte a CORS
- **pandas**: Manipulação de dados
- **numpy**: Cálculos numéricos
- **newsapi-python**: Integração com News API

### Dependências Completas
Veja o arquivo `requirements.txt` para a lista completa de dependências.

## Limitações e Considerações

### Dados Simulados
- O sistema atualmente usa dados simulados para demonstração
- Para uso em produção, integre com APIs de dados reais de mercado

### API de Notícias
- Requer chave da News API para notícias reais
- Sem a chave, usa análise de sentimento básica

### Ambiente de Desenvolvimento
- Configurado para desenvolvimento local
- Para produção, use um servidor WSGI adequado

## Próximos Passos

### Melhorias Sugeridas
1. **Integração com Dados Reais**: Conectar com APIs de corretoras
2. **Machine Learning**: Implementar modelos preditivos
3. **Backtesting**: Sistema de teste histórico
4. **Alertas**: Notificações por email/SMS
5. **Portfolio Management**: Gestão de múltiplos ativos

### Expansões Possíveis
1. **Suporte a Múltiplos Índices**: Bovespa, S&P 500, etc.
2. **Análise Fundamental**: Indicadores econômicos
3. **Social Trading**: Análise de redes sociais
4. **Mobile App**: Aplicativo móvel
5. **API Pública**: Disponibilizar como serviço

## Suporte e Contribuições

Este projeto foi desenvolvido como uma demonstração de conceito para automação de trading conservador. Para sugestões, melhorias ou questões técnicas, consulte a documentação do código ou entre em contato com a equipe de desenvolvimento.

## Licença

Este projeto é fornecido como está, para fins educacionais e de demonstração. Use por sua própria conta e risco em ambientes de produção.

---

**Desenvolvido por**: Manus AI  
**Versão**: 1.0.0  
**Data**: Julho 2025

