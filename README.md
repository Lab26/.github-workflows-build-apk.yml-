# E.V.E. Android — MVP 0.1

Primeira versão funcional de uma assistente Android com:
- perguntas por texto usando a OpenAI Responses API;
- ditado em português brasileiro usando o reconhecedor disponível no Android;
- leitura da resposta com TextToSpeech do Android;
- persona E.V.E. configurada no prompt.

## Limites desta versão
- **Não** implementa palavra de ativação contínua “EVE”. Para priorizar bateria, o usuário toca em **Falar** e dita a pergunta.
- Não escuta com a tela bloqueada.
- Não identifica chamadas nem reconhece rostos.
- A voz feminina depende das vozes instaladas/configuradas no Android; esta versão escolhe português (Brasil), mas não pode garantir timbre feminino em todos os aparelhos.
- A chave de API é guardada localmente em SharedPreferences para facilitar o protótipo. Isto não é adequado para distribuição pública: APKs podem ser analisados. Para uso real, coloque a chamada de API atrás de um servidor próprio e não distribua uma chave secreta no app.
- Uso da API é cobrado conforme a conta, modelo e utilização. A assinatura do ChatGPT não inclui automaticamente créditos de API.

## Requisitos
- Android 8.0 (API 26) ou superior.
- Android Studio recente com JDK 17 e SDK Android 35.
- Conexão à internet.
- Chave de API da plataforma OpenAI com faturamento/configuração habilitados.
- Microfone e permissão de gravação para ditado.

## Como compilar
1. Baixe e extraia o ZIP.
2. Abra a pasta `EVE_Android_MVP` no Android Studio (Open).
3. Aguarde o Gradle Sync. Se o Android Studio pedir para instalar Android SDK Platform 35 e Build Tools, aceite.
4. Conecte o Samsung ao PC por USB e habilite Opções do desenvolvedor > Depuração USB; ou use Build > Build APK(s).
5. Para gerar o APK: **Build > Build Bundle(s) / APK(s) > Build APK(s)**.
6. O APK de debug normalmente fica em `app/build/outputs/apk/debug/app-debug.apk`.
7. Copie para o telefone e abra o arquivo. Se solicitado, permita instalar apps dessa fonte. Instale apenas o APK que você mesmo compilou.

## Como usar
1. Abra E.V.E.
2. Cole sua chave de API OpenAI no campo de chave.
3. Digite uma pergunta e toque em **Perguntar**, ou toque em **Falar** e dite em português.
4. A resposta aparecerá na tela e será lida em voz alta.

## API
O app usa `POST https://api.openai.com/v1/responses`, com o modelo `gpt-4.1-mini`. Se esse modelo não estiver disponível para sua conta, altere a constante `model` em `MainActivity.kt` para um modelo habilitado na sua conta. Consulte a documentação oficial: https://developers.openai.com/api/docs/guides/text

## Segurança e privacidade
- O texto da pergunta é enviado à API OpenAI pela internet.
- A chave fica no armazenamento privado do app, mas sem proteção criptográfica adicional neste protótipo.
- Não inclua dados altamente sensíveis.
- A permissão de microfone só é solicitada para o ditado iniciado pelo usuário.
- Esta versão não inicia gravação silenciosa em segundo plano.

## Próximas etapas sugeridas
1. Migrar a chave para um backend seguro.
2. Melhorar a interface e histórico de conversas.
3. Adicionar streaming de respostas.
4. Avaliar APIs de voz neural para fala mais natural.
5. Projetar um recurso de palavra de ativação de baixo consumo, explicando claramente consumo de bateria e limitações de microfone em segundo plano no Android moderno.
