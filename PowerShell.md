# Tutorial: Como Usar o Comando Set-ExecutionPolicy RemoteSigned

## O que é o Set-ExecutionPolicy?

O `Set-ExecutionPolicy` é um comando do PowerShell que controla quais scripts podem ser executados no Windows. Por padrão, o Windows bloqueia a execução de scripts por questões de segurança.

## Por que usar RemoteSigned?

A política `RemoteSigned` é recomendada porque:
- Permite executar seus próprios scripts locais
- Protege contra scripts maliciosos da internet (exige assinatura digital)
- É o padrão recomendado para desenvolvedores

## Passo a Passo

### Passo 1: Abrir o PowerShell como Administrador

**Windows 10/11:**
1. Clique no botão Iniciar
2. Digite "PowerShell"
3. Clique com o botão direito em "Windows PowerShell"
4. Selecione "Executar como administrador"
5. Clique em "Sim" na janela de controle de conta de usuário

### Passo 2: Verificar a Política Atual (Opcional)

Antes de alterar, você pode verificar qual política está ativa:

```powershell
Get-ExecutionPolicy
```

### Passo 3: Executar o Comando

Digite o seguinte comando e pressione Enter:

```powershell
Set-ExecutionPolicy RemoteSigned
```

### Passo 4: Confirmar a Alteração

O sistema pedirá confirmação. Você verá uma mensagem como esta:

```
Alteração de Política de Execução
A política de execução ajuda a protegê-lo contra scripts não confiáveis...
Deseja alterar a política de execução?
[S] Sim  [N] Não  [U] Suspender  [?] Ajuda (o padrão é "N"):
```

Digite `S` e pressione Enter.

### Passo 5: Verificar se Funcionou

Confirme a alteração executando:

```powershell
Get-ExecutionPolicy
```

Deve retornar: `RemoteSigned`

## Políticas Disponíveis

- **Restricted**: Não permite execução de scripts (padrão)
- **AllSigned**: Todos os scripts precisam ser assinados
- **RemoteSigned**: Scripts remotos precisam ser assinados
- **Unrestricted**: Executa todos os scripts (menos seguro)
- **Bypass**: Nada é bloqueado, sem avisos

## Reverter a Alteração

Se precisar voltar à configuração padrão:

```powershell
Set-ExecutionPolicy Restricted
```

## Avisos de Segurança

⚠️ **Importante:**
- Só execute scripts de fontes confiáveis
- `RemoteSigned` oferece boa proteção, mas não é infalível
- Sempre revise scripts antes de executá-los
- Considere usar `AllSigned` para máxima segurança em ambientes corporativos

## Dicas

💡 **Dica 1:** Para projetos de desenvolvimento, usar `-Scope CurrentUser` é suficiente e não requer privilégios de administrador:
```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

💡 **Dica 2:** Se você precisa executar apenas um script específico sem alterar a política do sistema:
```powershell
PowerShell -ExecutionPolicy Bypass -File .\seu-script.ps1
```

💡 **Dica 3:** Para desbloquear um arquivo baixado da internet manualmente:
```powershell
Unblock-File -Path .\seu-script.ps1
```

💡 **Dica 4:** Verifique todas as políticas ativas em diferentes escopos:
```powershell
Get-ExecutionPolicy -List
```

## Solução de Problemas

### Erro: "Acesso Negado"
- Certifique-se de estar executando o PowerShell como Administrador

### Erro: "Set-ExecutionPolicy não é reconhecido"
- Você pode estar usando o Prompt de Comando (CMD) ao invés do PowerShell
- Abra o Windows PowerShell

### Script ainda não executa
- Verifique se o arquivo tem extensão `.ps1`
- Tente desbloquear o arquivo: clique com botão direito > Propriedades > Desbloquear

## Exemplo Prático

Depois de configurar, você pode executar um script assim:

```powershell
# Navegar até a pasta do script
cd C:\MeusProjetos

# Executar o script
.\meu-script.ps1
```
