# SLA e Infraestrutura no Microsoft Azure

Este repositório reúne um resumo sobre os Acordos de Nível de Serviço (SLA) da Microsoft Azure, explicando os principais tipos, como criar uma máquina virtual com boas práticas de disponibilidade, o conceito de zonas de disponibilidade e como funciona a redundância ao configurar uma conta de armazenamento.

---

## 🌐 O que é SLA?

SLA (Service Level Agreement) é basicamente um contrato de garantia da Microsoft sobre a **disponibilidade mínima** de um serviço no Azure. Ele define quanto tempo, em média, um serviço pode ficar disponível ao longo do mês.

### Exemplos práticos de SLA no Azure

| Serviço                    | SLA mensal estimado     |
|---------------------------|-------------------------|
| Máquina Virtual (isolada) | 99,9%                   |
| VM em duas zonas          | 99,99%                  |
| Armazenamento Blob (LRS)  | 99,9%                   |
| SQL Database              | 99,99%                  |

---

## 🧩 Tipos de SLA

- **SLA individual**: aplica-se a um único serviço. Ex: uma máquina virtual ou um banco de dados isolado.
- **SLA combinado**: quando usamos mais de um serviço (ex: App Service + Banco de Dados). O SLA final será o produto das probabilidades.
- **Alta disponibilidade com zonas**: usar Zonas de Disponibilidade melhora o SLA de alguns serviços (ex: VMs alcançam até 99,99%).

---

## ⚙️ Como criar uma Máquina Virtual no Azure

Aqui vai um passo a passo simplificado para criar sua primeira VM:

1. Acesse o portal: [portal.azure.com](https://portal.azure.com)
2. Vá em **Máquinas Virtuais** > clique em **Criar**
3. No formulário, preencha:
   - Nome da VM
   - Região (escolha uma com suporte a zonas, se possível)
   - Imagem do sistema (Windows, Ubuntu, etc.)
   - Tamanho (ex: Standard B2s)
4. Em "Disponibilidade", ative a opção para usar **Zonas de Disponibilidade** (se quiser mais resiliência).
5. Configure disco, rede e segurança conforme sua necessidade.
6. Clique em **Revisar + Criar** e aguarde a implantação.

---

## 🛰 O que são Zonas de Disponibilidade?

Zonas de Disponibilidade (ou *Availability Zones*) são datacenters fisicamente separados dentro de uma mesma região do Azure. Cada zona tem alimentação elétrica, rede e refrigeração independentes.

Por que isso importa?

Se uma zona tiver um problema (ex: queda de energia), as outras continuam funcionando. Ao distribuir sua aplicação entre duas ou mais zonas, você garante mais estabilidade — e melhora o SLA.

---

## 📦 Redundância ao criar uma conta de armazenamento

Quando você cria uma conta de armazenamento no Azure (para arquivos, blobs, tabelas, etc.), é necessário escolher um tipo de **replicação dos dados**. Isso define onde e como os dados serão copiados para evitar perda em caso de falha.

### Tipos de redundância:

| Tipo     | Como funciona                                                       | Indicado para...                           |
|----------|----------------------------------------------------------------------|--------------------------------------------|
| **LRS**  | Três cópias locais na mesma zona                                    | Uso geral com baixo custo                  |
| **ZRS**  | Cópias distribuídas entre zonas na mesma região                     | Alta disponibilidade dentro da região      |
| **GRS**  | Cópias em duas regiões geográficas (principal + secundária)         | Proteção contra desastres regionais        |
| **RA-GRS** | GRS com acesso de leitura à região secundária                      | Leitura contínua mesmo em caso de falha    |
