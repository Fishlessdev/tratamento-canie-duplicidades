# Tratamento de duplicidades da base CANIE

Notebook reprodutível para identificação, classificação, revisão e consolidação de possíveis registros duplicados da base CANIE.

## Visão geral

O fluxo combina evidências cadastrais, textuais, morfológicas, espaciais e temporais. Pares com evidência forte podem ser tratados automaticamente; situações ambíguas são encaminhadas para decisão manual documentada.

O notebook foi organizado em etapas pequenas, acompanhadas de documentação técnica e didática. As decisões de remoção permanecem auditáveis e a base original é preservada durante todo o processamento.

## Estrutura esperada

```text
.
├── 00_Tratamento_CANIE.ipynb
├── 01_bases/
│   └── arquivo_de_entrada.xlsx
└── 02_outputs/
```

A pasta `01_bases` deve conter exatamente uma planilha `.xlsx`. Arquivos temporários do Excel iniciados por `~$` são ignorados. Os produtos são gravados automaticamente em `02_outputs`.

As bases e os outputs não fazem parte do repositório. Cada usuário deve fornecer localmente a entrada autorizada para processamento.

## Produtos

O fluxo gera:

- base consolidada em Excel;
- relatório de auditoria com múltiplas abas;
- GeoPackage com registros, pares e grupos espacializados.

## Ambiente

Recomenda-se Python 3.11 ou versão compatível com as dependências geoespaciais utilizadas.

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
jupyter notebook 00_Tratamento_CANIE.ipynb
```

Também é possível utilizar um ambiente Conda para facilitar a instalação de GeoPandas, GDAL e PROJ.

## Decisões manuais

Os pares encaminhados para revisão são identificados por códigos `REV_MAN_...`. A decisão manual informa explicitamente qual CANIE deve ser removido. Essas escolhas são decisões metodológicas do autor com base nos dados disponíveis e podem exigir revisão documental ou verificação presencial em campo.

## Observações metodológicas

- Um par candidato não representa automaticamente uma duplicidade.
- Registros pendentes são preservados até que exista decisão explícita.
- Coordenadas ausentes não formam chaves espaciais artificiais.
- Grupos transitivos incluem apenas registros efetivamente conectados por pares.
- Registros marcados para remoção manual não podem ser escolhidos como principais.

## Privacidade e dados

Antes de compartilhar entradas ou produtos, verifique as condições de uso, licenciamento e eventual sensibilidade dos dados. O `.gitignore` impede o versionamento padrão das pastas de entrada e saída.
