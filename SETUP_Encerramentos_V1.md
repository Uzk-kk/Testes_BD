# Setup — Andamento de Encerramentos V1

## 1. Abas obrigatórias no mesmo Google Sheets

Crie as quatro abas abaixo exatamente com estes nomes.

### Encerramentos
UUID Processo | ID Processo | Tipo Processo | Loja | Apelidos da Loja | Data de Criação | Notificação | Data do envio da notificação | Data do fechamento | Contagem mercadoria | Data da contagem | Retirada mercadoria | Data da retirada | Desmobilização | Data da desmobilização | Retirada da fachada / comunicação visual | Data da retirada da com. visual | Contas de consumo | Data do envio das contas de consumo | Vistoria de devolução | Data da vistoria de devolução | Entrega das chaves | Data da entrega das chaves | Orçamentos enviados? | Adequações | Distrato contas a pagar | Data do envio para o contas a pagar | Distrato jurídico | Data do envio para o jurídico | Distrato aprovação | Data do envio do distrato para aprovação | Distrato | Contas pagamento | Data do envio da solicitação de pagamento para o contas a pagar | Para legal baixa no CNPJ | Próximo passo / observações | Estado do processo | Data de conclusão | Data de arquivamento | Arquivado por | Motivo do arquivamento | Cadastrado Por | Última Alteração Por | Data da Alteração

### Histórico Encerramentos
ID Histórico | UUID Processo | ID Processo | Loja | Data/Hora | Usuário | Nível | Tipo de ação | Campo alterado | Valor anterior | Valor novo | Detalhe

### Documentos Encerramentos
UUID Documento | ID Documento | UUID Processo | ID Processo | Loja | Categoria | Descrição | Nome original | Drive File ID | SHA-256 | Data do envio | Enviado Por | Tamanho (bytes) | Tipo MIME | Estado Documento | Excluído por | Data da exclusão

### Controle do Sistema
Chave | Valor | Atualizado em | Atualizado por

Não é necessário preencher nenhuma linha inicialmente. O sistema cria o contador `SEQ_ENC` ao cadastrar o primeiro encerramento.

## 2. Google Drive

O módulo de encerramentos funciona sem o Drive configurado. A área Documentos ficará em modo informativo até o OAuth ser configurado.

Quando formos configurar o OAuth, o `st.secrets` deverá conter esta seção:

```toml
[google_drive]
client_id = "SEU_CLIENT_ID"
client_secret = "SEU_CLIENT_SECRET"
refresh_token = "SEU_REFRESH_TOKEN"
token_uri = "https://oauth2.googleapis.com/token"
root_folder_id = ""
```

`root_folder_id` pode permanecer vazio. Nesse caso, o sistema cria/procura a pasta `Encerramentos - Sistema` no Drive autenticado.

Nunca coloque essas credenciais diretamente no arquivo Python.

## 3. Dependências adicionais

Instale as dependências de `requirements_encerramentos.txt` no mesmo ambiente do projeto.

## 4. Observação sobre PDF

A validação V1 verifica:
- extensão `.pdf`;
- MIME de PDF quando informado pelo navegador;
- assinatura binária `%PDF-` nos primeiros 1024 bytes;
- nome da loja ou apelido autorizado no nome do arquivo;
- SHA-256 para impedir duplicidade do mesmo conteúdo no mesmo processo.

Isso não é validação de assinatura digital ICP-Brasil; é validação estrutural do tipo de arquivo.
