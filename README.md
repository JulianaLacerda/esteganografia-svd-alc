# Esteganografia em Imagens Digitais utilizando Decomposição em Valores Singulares (SVD)

Trabalho da disciplina de Álgebra Linear Computacional — Graduação em
Matemática Computacional, UNIFESP.

**Autoras:** Ana Julia Barbosa Furtado, Bruna Pimentel, Juliana Duarte Lacerda
**Professor:** Dr. Luiz Leduíno Salles Neto

## Descrição

Este projeto implementa e compara dois métodos de esteganografia baseados na
Decomposição em Valores Singulares (SVD), inspirados no trabalho de Bergman e
Davidson (2005), *"Unitary Embedding for Data Hiding with the SVD"*:

- **Método 1 — Perturbação da Paridade de Σ**: insere bits da mensagem
  ajustando a paridade dos valores singulares menos significativos da
  imagem.
- **Método 2 — Rotação Ortogonal de U (*Unitary Embedding*)**: insere bits
  aplicando pequenas rotações de Givens a pares de colunas da matriz $U$,
  preservando $\Sigma$ integralmente. Requer uma chave externa para a
  extração (não é esteganografia cega).

Ambos os métodos foram avaliados quanto a imperceptibilidade (PSNR, SSIM),
capacidade, taxa de erro de extração, e robustez a quantização e
recompressão JPEG.

## Estrutura do repositório

```
.
├── Metodo1_Perturbacao_Sigma.ipynb   # Notebook do Método 1 (codificação + decodificação)
├── Metodo2_Rotacao_U.ipynb           # Notebook do Método 2 (codificação + decodificação)
├── DATA/
│   ├── Passaro.jpg                   # Imagem de teste 1
│   └── Paisagem.jpg                  # Imagem de teste 2
└── README.md
```

## Requisitos

- Python 3.10+
- Bibliotecas: `numpy`, `matplotlib`, `scikit-image`, `pillow`

Instalação:

```bash
pip install numpy matplotlib scikit-image pillow
```

## Como executar

### Opção 1 — Google Colab (recomendado, sem instalação local)

1. Abra o notebook desejado em [colab.research.google.com](https://colab.research.google.com)
2. Crie uma pasta `DATA` no painel de arquivos à esquerda
3. Faça upload de `Passaro.jpg` e/ou `Paisagem.jpg` para dentro dela
4. Execute as células em ordem (Run All, ou uma por uma)
5. Quando solicitado, digite a mensagem secreta a ser oculta

### Opção 2 — Jupyter local

```bash
jupyter notebook Metodo1_Perturbacao_Sigma.ipynb
```

Certifique-se de que a pasta `DATA/` está no mesmo diretório do notebook.

## Fluxo de cada notebook

1. **Codificação**: leitura da mensagem e da imagem → decomposição SVD →
   inserção dos bits → reconstrução da imagem esteganográfica → testes
   exploratórios de robustez (quantização, recompressão JPEG) e esteganálise
   simples (Método 1) ou verificação de preservação de Σ (Método 2)
2. **Decodificação**: leitura da imagem esteganográfica (e, no Método 2, da
   chave) → extração dos bits → reconstrução da mensagem → cálculo da taxa
   de erro de bits

## Principais resultados

| Método | Cego? | PSNR (dB) | Erro pós-quantização | Robusto a JPEG? |
|---|---|---|---|---|
| 1 (Σ) | Sim | 138–144 | 41–55% | Não |
| 2 (U) | Não (requer chave) | 65–76 | 0–0,83% | Inconsistente |

Detalhamento completo, incluindo diagnóstico de falhas por colisão de
valores singulares e discussão comparativa com o artigo de referência, no
relatório (`relatorio.pdf`).

## Referências

- BERGMAN, C.; DAVIDSON, J. *Unitary Embedding for Data Hiding with the
  SVD*. Security, Steganography, and Watermarking of Multimedia Contents
  VII, SPIE Vol. 5681, 2005.
- GOLUB, G.; VAN LOAN, C. F. *Matrix Computations*. 4th ed. Johns Hopkins
  University Press, 2013.
- GONZALEZ, R. C.; WOODS, R. E. *Digital Image Processing*. 4th ed.
  Pearson, 2018.
