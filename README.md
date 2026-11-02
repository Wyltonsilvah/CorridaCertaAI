# CorridaCerta AI — projeto Android experimental

## Estado real
Código-fonte de protótipo. **Não é APK compilado** e **não foi testado em Android real**. A meta de 4 segundos não está validada. Os testes locais executados verificam apenas o motor Kotlin de cálculo e interpretação de dois exemplos.

## Funções
- Serviço de acessibilidade opt-in para leitura de texto exposto por telas de ofertas Uber/Lalamove.
- Indicador flutuante, somente informativo, sem aceitar ou recusar ofertas.
- Custo por km, meta líquida por hora, minutos adicionais por entrega.
- Lalamove: soma deslocamento até coleta + rota; interpreta preço com adicional e múltiplas entregas.
- Estado DADOS INSUFICIENTES quando não houver tempo identificável.

## Compilar APK
1. Abra esta pasta no Android Studio recente, com Android SDK 35 e suporte a Kotlin/Gradle.
2. Aguarde a sincronização Gradle; em Build > Build APK(s), compile a variante debug.
3. Instale o APK debug no Android de teste. Ative manualmente o serviço CorridaCerta AI nas configurações de Acessibilidade.
4. Faça testes **sem dirigir**. Compare a oferta real com o que o app interpretou. O sistema pode falhar se as plataformas não expuserem os textos por acessibilidade, mudarem a interface ou restringirem sobreposições.

## Privacidade e limites
Não há transmissão de ofertas a servidores no código atual. Não há OCR de imagens, gravação oculta, histórico persistente, integração com mapas ou leitura automática de telas inacessíveis por acessibilidade. Não há garantias de compatibilidade com Uber/Lalamove nem de cumprimento de 4 segundos. Não usar como única base de decisão financeira. Custos por km são estimativas; pedágios e retorno vazio não são computados.

## Teste de lógica sem Android
`kotlinc app/src/main/java/br/com/corridacerta/OfferAnalyzer.kt tests/AnalyzerSmoke.kt -include-runtime -d teste.jar && java -jar teste.jar`


## Modo resposta rápida (v0.3 experimental)
- Serviço de acessibilidade monitora eventos de alteração de janela e conteúdo enquanto habilitado; não precisa abrir a calculadora a cada oferta.
- notificationTimeout=0 e limite de varredura de 80 ms; **não** representa garantia de decisão em 80 ms.
- O processamento matemático é local, sem requisição à internet.
- Se a Uber/Lalamove desenhar os dados sem expô-los à acessibilidade, a leitura falhará; será preciso um caminho alternativo de captura de tela autorizada e OCR local.
- Não há aceite ou recusa automática. Sem testes de dispositivo, o tempo total de ponta a ponta não é conhecido.
- Não registrar dados pessoais das telas em logs.
