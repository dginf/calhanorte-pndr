# Painel de Indicadores da PNDR

## Estrutura do repositório

```
painel-pndr/
├── index.html
├── .gitattributes       ← configuração do Git LFS
└── dados/
    ├── db.json          ← série histórica por região
    ├── municipios.json  ← 5.570 municípios (LFS)
    ├── det.json         ← indicadores 2024 por município (LFS)
    ├── det_serie.json   ← série 2013-2024 por município (LFS, 44MB)
    ├── pnad.json        ← PNAD Contínua
    ├── geo.json         ← mapa SVG
    ├── nr.json          ← novos recortes
    └── perc.json        ← percentis
```

## Primeiro setup (uma única vez)

```bash
# 1. Instalar Git LFS
git lfs install

# 2. Clonar ou criar o repositório
git clone https://github.com/SEU_USUARIO/painel-pndr
cd painel-pndr

# 3. Rastrear arquivos grandes
git lfs track "dados/det_serie.json"
git lfs track "dados/det.json"
git lfs track "dados/municipios.json"

# 4. Adicionar e commitar tudo
git add .gitattributes
git add .
git commit -m "Painel PNDR - versão inicial"
git push origin main
```

## Atualizar dados (quando tiver novo banco)

```bash
# Rodar o script de geração de dados
python gerar_dados.py dados_reduzido.db

# Subir só os arquivos que mudaram
git add dados/
git commit -m "Atualização de dados - [data]"
git push origin main
```

## Git LFS no GitHub Pages

O GitHub Pages serve arquivos LFS normalmente via URLs públicas.
O `fetch()` no index.html funciona sem nenhuma configuração adicional.

## Limites do Git LFS (plano gratuito)

- Armazenamento: 1GB
- Banda: 1GB/mês
- Para uso interno do MIDR, considerar GitHub Enterprise ou plano pago.
