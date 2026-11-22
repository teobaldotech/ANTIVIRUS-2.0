# 🛡️ NeonAV Secure PRO ULTRA 2.0

Aplicação web em **HTML5, CSS3 e JavaScript (ES6+)** voltada para análise estática local de arquivos, inspeção lexical de URLs, simulação educativa de perímetro WAF/IPS e execução de **11 testes automatizados** diretamente no navegador, sem dependências externas.

Desenvolvido por **Teobaldo Machado Batista Ribeiro** (`teobaldotech`) como projeto de portfólio em desenvolvimento web front-end e segurança defensiva.

---

## ✨ Principais Funcionalidades

### 1. Scanner Estático Local (`Análise Real`)
* **Hash Criptográfico SHA-512:** Calcula o digest completo via Web Crypto API (`crypto.subtle.digest("SHA-512", ...)`).
* **Entropia de Shannon:** Mede a distribuição de bytes (`0` a `8` bits/byte) para sinalizar conteúdos potencialmente compactados, cifrados ou ofuscados.
* **Assinatura Binária & Extensões:** Identifica cabeçalhos conhecidos (`MZ/PE`, `ELF`, `ZIP/APK/JAR`, `PDF`), extensões executáveis/de script e indícios de dupla extensão.
* **Heurísticas & Extração de IOCs:** Avalia padrões textuais suspeitos (captura de senha, ação externa em formulário, `keydown`, `document.cookie`, `sendBeacon`, `eval`/`atob`, PowerShell, comandos de shell e persistência) e extrai URLs e endereços IPv4 embutidos.
* **Análise Estrutural de URL:** Valida sintaxe e protocolo (`http:` / `https:`) sem emitir requisições remotas, pontuando sinais como uso de IP direto no host, `xn--` (Punycode), `@`, TLDs frequentes em campanhas descartáveis, excesso de subdomínios e termos sensíveis.
* **Exportação de Laudos:** Gera relatórios em **JSON**, **CSV** (com escape adequado de aspas e delimitadores) e **HTML**.

### 2. Firewall / IPS (`Simulação Educativa`)
* Simula o comportamento de regras de mitigação para **DDoS**, **XSS**, **SQL Injection** e **Brute Force**, utilizando endereços da faixa reservada **RFC 5737 (`203.0.113.0/24`)**.
* Separa visualmente os eventos simulados da análise estática real, deixando explícito que um navegador em sandbox não intercepta tráfego de rede do sistema operacional.

### 3. Suíte de Testes Automatizados (`11 Testes QA`)
Executa asserções reais na interface sem necessidade de runner externo, cobrindo:
1. Sanitização XSS com `escapeHTML`.
2. Validação de entrada de URL (bloqueio de esquemas inválidos como `javascript:` e aceite de URLs `https:`).
3. Validação de tamanho máximo de arquivo.
4. Cálculo de entropia de Shannon em distribuição uniforme.
5. Geração de hash SHA-512 (128 caracteres hexadecimais).
6. Pontuação heurística em amostra sintética suspeita.
7. Classificação de risco baixo em amostra limpa.
8. Faixas e limites de `classifyRisk` (`0–24`, `25–49`, `50–74`, `75–100`).
9. Ordenação decrescente por `score` e `size` em `sortReports`.
10. Filtros por nível de risco, hash e IOC em `filterReports`.
11. Serialização e escape de aspas em `buildJSONExport` e `buildCSVExport`.

---

## 🧱 Estrutura e Organização

O projeto é entregue como aplicação single-file (`index.html`) com tema escuro, capa inicial com ações diretas, suporte responsivo para desktop e dispositivos móveis (como Android/Chrome) e persistência local via `localStorage` com validação na leitura.

* **Camada de UI & Navegação:** Capa inicial (`#coverScreen`), abas (`Scanner Estático`, `Firewall / IPS`, `Testes Automatizados`), filtros, barras de progresso e modal de amostras sintéticas (`[AMOSTRA SINTÉTICA]`).
* **Camada de Validação & Domínio:** `validateURLInput`, `validateFileInput`, `analyzeFileBuffer`, `analyzeURLStatic`, `classifyRisk`, `filterReports`, `sortReports`, `buildJSONExport` e `buildCSVExport`.
* **Camada de QA:** `runAutomatedTestSuite` com contagem de aprovados/falhas e tempo de execução em milissegundos.

---

## 🚀 Como Executar

1. Baixe ou clone o repositório de `teobaldotech`.
2. Abra o arquivo `index.html` diretamente em um navegador moderno (Chrome, Edge, Firefox ou Android Chrome) ou sirva via servidor local estático.
3. Na capa inicial, clique em **🚀 Acessar Painel 2.0**, **🧪 Abrir Amostras Sintéticas** ou **⚙️ Executar 11 Testes Automatizados**.

---
