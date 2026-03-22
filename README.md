# 📦 Sistema de Logística e Infraestrutura - Comissão Firjan SESI

![Google Apps Script](https://img.shields.io/badge/Google%20Apps%20Script-4285F4?style=for-the-badge&logo=google&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)

> Uma aplicação web *serverless* de custo zero, desenvolvida nativamente no ecossistema Google Workspace para a gestão logística em tempo real de grandes eventos (Festival Multicultural e RecuperARTE).

---

## 📸 Demonstração do Sistema

*(DICA: Arraste e solte uma imagem ou GIF do seu painel a funcionar aqui para o GitHub carregar a imagem)*

---

## 📋 Sobre o Projeto

Este sistema foi criado para resolver o desafio de coordenar a entrega de infraestrutura (mesas, cadeiras, pontos de energia, banners) e a gestão de turmas/oficinas durante os eventos da Comissão Firjan SESI. 

Em vez de utilizar servidores pagos e bases de dados complexas, o projeto utiliza o **Google Apps Script** para transformar uma planilha do Google Sheets numa API robusta e num painel web interativo. O foco principal da arquitetura foi garantir **alta disponibilidade, resiliência contra falhas de internet e otimização extrema da cota de processamento do Google**.

---

## ✨ Principais Funcionalidades

* **📊 Dashboard de KPIs em Tempo Real:** Visão global de itens pedidos vs. entregues.
* **💾 Sistema de Rascunho (Drafts) com Deteção de Conflitos:** Se o utilizador digita um valor e outro membro da equipa atualiza o banco de dados antes do salvamento, o sistema não apaga o que foi digitado, mas exibe um alerta visual (`⚠️ Oficial: X`), permitindo descartar ou sobrescrever.
* **🔄 Atualização Silenciosa (Smart Polling):** O sistema busca novos dados no servidor a cada 20 minutos sem recarregar a tela, protegendo o foco do utilizador caso ele esteja digitando.
* **⏱️ Relógio de Sincronização Local:** Indicador visual de frescor dos dados (*"Atualizado há 3 minutos"*) sem consumir requisições do servidor.
* **🖨️ Geração de Relatórios em PDF:** Criação de listas de presença e checklists de logística prontos para impressão, utilizando a técnica de *Iframe Oculto* para contornar bloqueios nativos de pop-ups do Google Apps Script.
* **🛡️ Proteção Anti-Spam e Cooldown:** Botões de ação bloqueiam imediatamente após o clique (ex: *"A gravar..."*), impedindo envios duplicados e sobrecarga no servidor.
* **📱 Persistência de Estado (LocalStorage):** O sistema memoriza a URL do evento, os filtros selecionados (Área/Status) e os rascunhos localmente no navegador.

---

## 🧠 Destaques de Engenharia e Arquitetura

### 1. Evasão de Limites de Cota (Stress Tested)
O Google Apps Script possui limites diários de execução (90 a 360 minutos de tempo de servidor). O sistema foi arquitetado para dividir o processamento, unindo um intervalo de *polling* otimizado (20 min) com *cooldowns* manuais (60s), garantindo que uma equipa de 15 pessoas operando por 20 horas consuma uma fração ínfima da cota diária.

### 2. Resolução de Conflitos Cross-Site (iOS/Safari)
Para evitar o bloqueio de "Prevenção de Rastreamento entre Sites" nativo da Apple (que causa o erro *Too many redirects* ou *Drive Negado*), a implantação do sistema é configurada estrategicamente, dispensando a exigência de cookies de terceiros no navegador do cliente final.

---

## 🚀 Como Instalar e Executar

Siga os passos abaixo para implantar o sistema no seu ambiente Google Workspace:

1. **Preparação da Base de Dados**
   * Crie uma nova planilha no Google Sheets ou abra a existente com os dados do evento.
2. **Ambiente de Desenvolvimento**
   * Na sua planilha, vá ao menu **Extensões > Apps Script**.
   * Crie dois ficheiros principais:
     * `Codigo.gs` *(cole aqui as funções de backend em JavaScript)*.
     * `Index.html` *(cole aqui o código de frontend)*.
3. **Implantação (Deploy)**
   * No canto superior direito, clique em **Implantar > Nova implantação**.
   * Selecione o tipo **App da Web** (ícone de engrenagem ⚙️).
4. **Configurações Cruciais de Segurança**
   * **Executar como:** `Eu (seu_email@dominio.com)` *(Evita problemas de permissão de Drive e bloqueios no Safari/iOS).*
   * **Quem pode acessar:** `Qualquer pessoa` *(Libera o acesso sem exigir login, eliminando redirecionamentos).*
5. **Acesso**
   * Clique em **Implantar** e copie o URL gerado (terminado em `/exec`).
   * Abra o link gerado, cole a URL da sua planilha no ecrã de Setup e comece a operar!

---

## 📱 Interface Responsiva

O CSS foi construído do zero utilizando boas práticas de Design System (CSS Variables) para facilitar a manutenção de cores e temas. O layout adapta-se perfeitamente a iPads e ecrãs de telemóveis, facilitando o uso pela equipa de logística que está a caminhar pelo evento.

<br>

---
*Feito com dedicação para a otimização de processos logísticos da **Comissão Firjan SESI**.*
