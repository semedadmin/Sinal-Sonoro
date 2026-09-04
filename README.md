# Sinal Sonoro

Aplicativo para Windows que agenda e reproduz músicas automaticamente em dias e horários definidos. Indicado para escolas, empresas, eventos, avisos musicais e ambientes que precisam de reprodução programada.

![Java](https://img.shields.io/badge/Java-21-ED8B00?logo=openjdk&logoColor=white)
![Windows](https://img.shields.io/badge/Windows-10%20%7C%2011-0078D4?logo=windows)
![Versão](https://img.shields.io/badge/versão-4.1.0-2563EB)

> **Responsável pela publicação:** Secretaria Municipal de `[NOME DO MUNICÍPIO]`  
> **Plataforma:** Windows 10 e Windows 11 — 64 bits

## Download oficial

[![Baixar Sinal Sonoro](https://img.shields.io/badge/BAIXAR-Sinal%20Sonoro-2563EB?style=for-the-badge&logo=windows&logoColor=white)](https://github.com/ORGANIZACAO/sinal-sonoro/releases/latest/download/Sinal-Sonoro-Windows.exe)

**Versão atual:** 4.1.0  
**Tamanho aproximado:** 64 MB  
**Sistema:** Windows 10 ou Windows 11, 64 bits

Se o botão não funcionar, abra a página de [versões publicadas](https://github.com/ORGANIZACAO/sinal-sonoro/releases/latest).

> Antes de publicar, substitua `ORGANIZACAO` nos dois links acima pelo usuário ou organização oficial do GitHub. Substitua também `[NOME DO MUNICÍPIO]` pelo nome correto.

## Baixar e instalar

1. Clique no botão **Baixar Sinal Sonoro** acima.
2. Aguarde o download de `Sinal-Sonoro-Windows.exe`.
3. Feche uma versão anterior do programa.
4. Execute o instalador baixado.
5. Abra o Sinal Sonoro uma vez para ativar sua inicialização automática com o Windows.

O instalador inclui o runtime Java. O computador de destino não precisa ter Java, Maven ou outras ferramentas instaladas.

> O executável distribuído atualmente não possui certificado comercial de assinatura de código. O Windows pode exibir o SmartScreen. Confira a origem do download e o hash SHA-256 informado na Release antes de executá-lo.

## Funcionalidades

- Agendamento por horário e dias da semana.
- Execução automática mesmo quando o programa é aberto no meio de uma janela ativa.
- Horários que atravessam a meia-noite.
- Playlists formadas a partir de uma pasta e suas subpastas.
- Reprodução sequencial ou aleatória.
- Repetição opcional da playlist.
- Volume configurável por tarefa.
- Aumento gradual de volume entre 0 e 30 segundos.
- Botão **Tocar agora** para teste imediato.
- Importação de tarefas em JSON.
- Novas tentativas automáticas quando a reprodução não consegue iniciar.
- Pastas protegidas são ignoradas sem interromper a procura pelas músicas.
- Registro de diagnóstico em arquivo de log.
- Execução contínua na bandeja ao fechar ou minimizar a janela.
- Inicialização automática e oculta ao entrar no Windows.
- Proteção contra duas instâncias que poderiam reproduzir o mesmo sinal simultaneamente.

## Execução em segundo plano

Depois da primeira abertura da versão instalada, o Sinal Sonoro é cadastrado na inicialização do usuário do Windows. Nos próximos logins, ele inicia oculto na bandeja e começa imediatamente a monitorar todas as tarefas ativas.

- Fechar ou minimizar a janela não interrompe o agendador.
- Clique no ícone próximo ao relógio do Windows para abrir novamente.
- O menu do ícone permite iniciar, parar ou encerrar o programa.
- Use **Encerrar** no menu da bandeja quando realmente quiser finalizar o processo.

## Formatos de áudio

| Formato | Extensão | Observação |
|---|---|---|
| MP3 | `.mp3` | Recomendado para melhor compatibilidade |
| WAV | `.wav` | Áudio sem compressão |
| MPEG-4 Audio | `.m4a` | Depende do codec disponível no Windows |
| AAC | `.aac` | Depende do codec disponível no Windows |

## Como usar

### Criar uma tarefa

1. Clique em **Nova tarefa**.
2. Informe um nome e selecione a pasta de músicas.
3. Defina os horários de início e término.
4. Marque os dias da semana.
5. Ajuste o volume e o aumento gradual.
6. Salve a tarefa.

O monitoramento começa automaticamente ao abrir o programa. Para confirmar o áudio antes do horário, selecione a tarefa e clique em **Tocar agora**.

### Importar tarefas

Clique em **Importar JSON** e selecione um arquivo neste formato:

```json
{
  "tarefas": [
    {
      "nome": "Sinal da manhã",
      "pasta_musicas": "C:\\SinalSonoro\\Musicas",
      "hora_inicio": "08:00",
      "hora_fim": "08:05",
      "dias_semana": ["segunda", "terca", "quarta", "quinta", "sexta"],
      "ativo": true,
      "embaralhar": false,
      "repetir": false,
      "volume": 0.8,
      "fade_in_seconds": 5
    }
  ]
}
```

Ao importar, o aplicativo pergunta se tarefas existentes com o mesmo nome devem ser substituídas. Registros inválidos são ignorados e apresentados no relatório final.

## Dados e diagnóstico

As configurações do usuário não ficam dentro da pasta de instalação:

```text
%APPDATA%\MusicScheduler\
├── music_scheduler_config.json
└── scheduler.log
```

Ao atualizar ou reinstalar o aplicativo, as tarefas são preservadas. Se uma música não tocar, confira `scheduler.log` e verifique se a pasta ainda está acessível.

## Compilar localmente

Requisitos para desenvolvimento:

- Windows 10 ou 11;
- JDK 21 completo;
- PowerShell;
- conexão com a internet na primeira compilação.

Execute:

```powershell
.\build-installer.ps1
```

O script baixa Maven e WiX localmente quando necessário, executa os testes e cria:

```text
release\Sinal Sonoro-4.1.0.exe
```

Para apenas compilar e testar, com Maven instalado:

```powershell
mvn clean test
mvn package
```

## Publicar uma versão pelo GitHub

O workflow em `.github/workflows/release.yml` gera o instalador em um computador Windows do GitHub.

1. Atualize a versão no `pom.xml`, em `Main.java` e em `build-installer.ps1`.
2. Faça commit das alterações.
3. Crie e envie uma tag correspondente:

```bash
git tag v4.1.0
git push origin v4.1.0
```

O GitHub Actions executará os testes, criará uma Release e anexará o instalador `.exe`. Também é possível iniciar a automação manualmente pela aba **Actions**.

Além do arquivo com a versão no nome, a automação publica `Sinal-Sonoro-Windows.exe`. Esse nome fixo permite que o endereço usado pelo site institucional permaneça igual em todas as versões.

## Link para o site da Secretaria

Depois de substituir `ORGANIZACAO`, use este endereço no botão de download do site:

```text
https://github.com/ORGANIZACAO/sinal-sonoro/releases/latest/download/Sinal-Sonoro-Windows.exe
```

Exemplo HTML:

```html
<a
  href="https://github.com/ORGANIZACAO/sinal-sonoro/releases/latest/download/Sinal-Sonoro-Windows.exe"
  class="botao-download"
  aria-label="Baixar o instalador do Sinal Sonoro para Windows"
>
  Baixar Sinal Sonoro para Windows
</a>
```

CSS opcional para o botão:

```css
.botao-download {
  display: inline-block;
  padding: 0.85rem 1.25rem;
  border-radius: 0.5rem;
  background: #1d4ed8;
  color: #fff;
  font-weight: 700;
  text-decoration: none;
}

.botao-download:hover,
.botao-download:focus-visible {
  background: #1e40af;
  color: #fff;
}
```

## Estrutura

```text
.
├── .github/workflows/release.yml
├── src/main/java/br/com/sinalsonoro/
│   ├── AudioPlayer.java
│   ├── Main.java
│   ├── SchedulerService.java
│   ├── Task.java
│   └── TaskStore.java
├── src/main/resources/icons/
├── src/test/java/br/com/sinalsonoro/
├── build-installer.ps1
└── pom.xml
```

## Segurança e limitações

- Uma tarefa só pode reproduzir arquivos que o usuário do Windows consiga acessar.
- O computador precisa estar ligado e a sessão do usuário do Windows precisa ter sido iniciada. O Sinal Sonoro abre automaticamente na bandeja.
- O aplicativo não altera automaticamente o volume geral do Windows.
- Certificados comerciais de assinatura não estão incluídos no projeto.

## Versão atual

**4.1.0** — inclui execução na bandeja, inicialização automática com o Windows, proteção contra instâncias duplicadas, importação JSON e aumento gradual de volume.
