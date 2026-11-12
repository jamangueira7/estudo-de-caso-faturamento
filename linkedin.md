# Post para o LinkedIn

> Imagem sugerida para anexar: `img/linkedin-card.png` (1200×627). Gráficos de apoio para um carrossel: `img/01-kpis-tempo-por-os.png`, `img/08-volume-mensal.png`, `img/10-os-sem-log.png`, `img/07-fluxo-faturamento.png`.

---

## Versão principal (cerca de 2.300 caracteres, abaixo do limite de 3.000)

Faturamento é a receita da empresa. E o nosso dependia de uma fila opaca, de mexer direto no banco e no ERP quando algo falhava e de falhas que ninguém conseguia rastrear.

Nos últimos 2 anos, eu reconstruí esse processo em duas gerações, no painel interno da empresa onde trabalho. A 2ª geração (um serviço central com três robôs encadeados) está rodando em produção. Medido nos logs de produção, só o tempo de máquina:

📉 Criar a OS: −58% na mediana (12 → 5 min) e −63% no p90 (90% das OS prontas em até 22 min, antes 60)
📉 Faturar no ERP: −42% na mediana (26 → 15 min) e −54% no p90
🔎 Alterações sem log de auditoria: de ~37% das OS para ~0%
🔄 163 mil boletos conciliados automaticamente

O que mudou, na prática:

1️⃣ Uma fila virou uma cadeia de robôs, cada um com uma responsabilidade (criar OS → faturar → sincronizar → conciliar boleto).
2️⃣ Cada passo registra o estado e grava um log "de/para". Se uma OS falha, sabemos em qual etapa parou e dá para reprocessar pela tela.
3️⃣ Validações antes de enviar ao ERP (OS já existente, tamanho de campo, CPF/CNPJ) acabaram com o retrabalho e as notas duplicadas.

Três cuidados que eu tomei com os números e que valem contar:

• Tirei a espera humana da conta. Hoje as OS são geradas antes e faturadas nos dias 01 e 20; se eu medisse de ponta a ponta, o sistema pareceria mais lento por uma decisão de processo.
• 80% das falhas da 2ª geração vieram de dois episódios externos: a reforma tributária (primeiro o ERP exigindo o cadastro prévio dos serviços, depois a mudança de alíquotas somada a erro de cadastro manual, com clientes sem e-mail). Nesse segundo caso, o sistema passou a corrigir o cadastro sozinho e refaturar: 325 das 326 OS afetadas foram faturadas em até ~7 h, sem intervenção. Fora esses episódios, a taxa de erro é inferior a 1%.
• Descobri, usando o log, que de 37% a 56% das OS de alguns meses eram geradas por engano e canceladas. Sem elas, o volume é estável (~1.800/mês). Agora isso é uma métrica de qualidade.

O maior ganho não é só velocidade: é confiabilidade. Sem log, não existe melhoria provada.

Estudo completo, com método e limites da medição, no primeiro comentário 👇

#Laravel #PHP #Automação #Faturamento #Observabilidade #EngenhariaDeSoftware #Backend

---

## Versão curta (cerca de 700 caracteres)

Faturamento é receita, e o nosso era uma fila opaca, com falhas que ninguém rastreava.

Reconstruí o processo no painel interno da empresa onde trabalho: uma cadeia de robôs, com estado e log de auditoria em cada passo.

Medido nos logs de produção (só tempo de máquina), 2ª geração × 1ª:
📉 Criar a OS: −58% na mediana (12 → 5 min)
📉 Faturar no ERP: −42% na mediana
🔎 Alterações sem log: de ~37% das OS para ~0%
🔄 163 mil boletos conciliados

O maior ganho é confiabilidade, e não só velocidade.

#Laravel #PHP #Automação #EngenhariaDeSoftware

---

## Primeiro comentário (para o link do estudo completo)

Estudo completo, com método, gráficos e limites da medição: [inserir o link do .md ou do PDF]

Se você mexe com integração de ERP, faturamento ou robôs em Laravel, vale trocar uma ideia nos comentários.

---

## Roteiro de carrossel (opcional, 6 slides)

1. **Capa:** "Faturamento: 2ª geração, mais rápida e previsível" (`linkedin-card.png`)
2. **O problema:** fila opaca, intervenção manual no banco e no ERP, ciclos de dias.
3. **A solução:** diagrama dos robôs (`07-fluxo-faturamento.png`).
4. **O resultado:** criar a OS −58%, faturar no ERP −42% (`01-kpis-tempo-por-os.png`).
5. **O achado nos logs:** 37% a 56% das OS de alguns meses eram erradas (`08-volume-mensal.png`).
6. **O aprendizado:** "Sem log, não existe melhoria provada" e a rede de testes.

---

## Notas para você antes de postar

* **Comparação equivalente de "faturar".** O status 4 da 1ª geração significava "aguardando NF" (conferido no código) e corresponde ao status 13 da 2ª. O preenchimento da NF só é medido na 2ª geração, e o post não promete nada sobre esse trecho.
* **Enquadramento.** Os números comparam a 1ª e a 2ª geração do seu trabalho, e não o processo anterior a set/2024, que não tem tempo medido. O post diz isso ("duas gerações") de propósito, para não ser contestado.
* **Anonimização.** O post e o estudo não citam o nome da empresa, o ERP, o CRM nem os nomes dos robôs (usam descrições como "robô que cria a OS"). Mesmo assim, confirme com a empresa se pode divulgar números de produção.
* Os números são agregados, sem clientes, valores ou documentos.
* "163 mil boletos" é a soma desde out/2024, e inclui a carga inicial de 115 mil.
* O trecho sobre OS geradas por engano é um piso: OS excluídas do banco antes do controle por status não aparecem.
