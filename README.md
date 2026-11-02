# shade·studio

> Uma cor. Oito profundidades.

![Arquivo único](https://img.shields.io/badge/arquivo-único-8d6c98?style=flat-square)
![Dependências](https://img.shields.io/badge/build-nenhum-8d6c98?style=flat-square)
![Tema](https://img.shields.io/badge/tema-claro%20%2F%20escuro-8d6c98?style=flat-square)

Gerador de paletas de sombras em **um único arquivo HTML**. Sem npm, sem build, sem backend. Você escolhe uma cor base e recebe uma escala de 8 sombras, pronta para copiar e usar.

---

## A história

Tudo começou com uma cor: `#E8C5E6`, um lilás claro.

Era a cor certa para o fundo de um card, mas faltava profundidade. O texto precisava de uma versão mais escura. O botão pedia outra. A borda, outra ainda. A sombra de um ícone, mais uma.

O caminho de sempre era abrir o editor de cores, arrastar o controle de luminosidade até "parecer bom" e repetir isso a cada cor nova. As escalas saíam inconsistentes de um projeto para o outro.

O Shade Studio faz esse passo uma vez e de forma previsível: **mesma cor base, mesma lógica, mesmo resultado**. Dá para trocar de cor, de tema ou de formato e a escala continua coerente.

---

## O que ele faz

| | |
|---|---|
| **8 sombras** | Da mais sutil (`Sombra 01`) à mais abissal (`Sombra 08`), numa única escala. |
| **Qualquer formato de entrada** | HEX, RGB, HSL, HSV, CMYK ou nome CSS. Cole e pronto. |
| **Seletor visual** | Caixa de saturação e barra de matiz, com [iro.js](https://iro.js.org). |
| **Intensidade ajustável** | Um slider deixa a escala mais suave ou mais marcada. |
| **Tema claro e escuro** | Segue o sistema, lembra sua escolha e anima a troca. |
| **Contraste na hora** | Cada sombra mostra a razão de contraste e o selo AA ou AAA. |
| **Exportação** | CSS variables, JSON ou lista de HEX, em um clique. |
| **Prévia em contexto** | Veja as sombras aplicadas a uma interface de exemplo. |
| **Atalhos** | `R` gera cor aleatória, `T` troca o tema, `1` a `8` copiam cada sombra. |

---

## Como usar

1. Baixe o `shade-studio.html`.
2. Abra no navegador (duplo clique).
3. Escolha uma cor e copie o que precisar.

Não há nada para instalar. As únicas dependências externas, as fontes do Google Fonts e o iro.js, vêm por CDN. Sem internet, o app funciona com fontes do sistema e cai no seletor de cor nativo do navegador.

---

## Formatos aceitos

Cole qualquer um destes no campo principal. A paleta atualiza enquanto você digita:

```
#E8C5E6             fff
rgb(232, 197, 230)  232 197 230
hsl(300, 47%, 85%)
hsv(300, 15%, 91%)  hsb(...)
cmyk(0%, 15%, 1%, 9%)
hotpink
```

Abaixo do campo há abas **HEX · RGB · HSL · HSV · CMYK** com um campo por canal. Mexer em qualquer número atualiza a paleta ao vivo. O botão **copiar** leva a cor no formato da aba ativa.

> Conversões entre formatos são arredondadas (1 unidade de diferença é normal). A paleta sempre usa a cor exata.

---

## Como as sombras são calculadas

A lógica é simples e previsível: **cada sombra é a cor base misturada com preto numa proporção fixa**.

```js
const FACTORS = [.06, .13, .21, .30, .40, .51, .63, .76];
const k = intensidade / 38;               // slider: 20 a 60, padrão 38

sombra[i] = cor_base × (1 − min(.94, FACTORS[i] × k))
```

Com a intensidade padrão e a base `#E8C5E6`:

| Nível | Nome | HEX |
|---|---|---|
| Base | | `#E8C5E6` |
| 01 | Sutil | `#DAB9D8` |
| 02 | Leve | `#CAABC8` |
| 03 | Suave | `#B79CB6` |
| 04 | Média | `#A28AA1` |
| 05 | Firme | `#8B768A` |
| 06 | Densa | `#726171` |
| 07 | Profunda | `#564955` |
| 08 | Abissal | `#382F37` |

Os passos são mais curtos nas sombras claras e mais longos nas escuras. Assim a escala parece uniforme ao olho, e não só nos números.

---

## Casos de uso

**Design de interfaces**
Gere a escala de uma cor de marca e use as sombras para hover, estados pressionados, bordas, divisores e texto secundário. Exporte como CSS variables e cole no projeto.

**Dark mode**
Use as sombras profundas (05 a 08) como superfícies e fundos de um tema escuro derivado da mesma cor base.

**Ilustração e pixel art**
Cada objeto precisa de luz, meio-tom e sombra. A escala dá uma rampa consistente para sombreamento.

**Ícones e logos**
Crie variações de uma cor mantendo a identidade, para ícones com profundidade ou versões monocromáticas.

**Apresentações e documentos**
Monte uma paleta coerente a partir de uma única cor, sem sair de um tom harmônico.

**Aprendizado**
Para quem estuda cor: dá para ver o efeito de escurecer uma cor em tempo real e comparar com a conversão entre RGB, HSL, HSV e CMYK.

---

## Exportação

**CSS variables**

```css
:root {
  --color-base: #E8C5E6;
  --shade-1: #DAB9D8;
  --shade-2: #CAABC8;
  /* ... até --shade-8 */
}
```

**JSON**

```json
{
  "base": "#E8C5E6",
  "shades": [
    { "name": "shade-1", "color": "#DAB9D8" },
    { "name": "shade-2", "color": "#CAABC8" }
  ]
}
```

**Lista HEX**, um código por linha, para colar em qualquer ferramenta.

---

## Atalhos

| Tecla | Ação |
|---|---|
| `R` | Cor aleatória |
| `T` | Alternar tema claro e escuro |
| `1` a `8` | Copiar a sombra correspondente |
| `Esc` | Fechar o seletor de cor |
| `Enter` | Confirmar o campo de cor |

---

## Acessibilidade

- Cada sombra escolhe sozinha texto claro ou escuro, conforme a luminância.
- O contraste (WCAG) aparece ao passar o mouse: **AA** a partir de 4,5:1 e **AAA** a partir de 7:1.
- Respeita `prefers-reduced-motion`: as animações são desativadas para quem pede isso.
- Os controles têm rótulos para leitores de tela e o foco aparece de forma clara.

---

## Stack

- **HTML, CSS e JavaScript puros**, sem framework e sem build
- **[iro.js](https://iro.js.org) 5.5.2**, para o seletor de cor
- **Google Fonts**: Manrope, DM Sans e DM Mono
- `localStorage` para lembrar o tema

Funciona nos navegadores atuais (Chrome, Edge, Firefox e Safari). A transição suave de tema usa a View Transitions API quando existe e cai numa troca simples quando não.

---

## Personalizando

**Mudar a escala:** edite a lista `FACTORS` no script. Mais valores, mais sombras (ajuste também `NAMES` e o layout da grade).

**Mudar a cor padrão:** altere `DEF` no começo do script.

**Mudar o visual:** todas as cores da interface são variáveis CSS no topo do arquivo (`--bg`, `--panel`, `--ink`, `--accent`...), em `:root` para o tema claro e em `[data-theme=dark]` para o escuro.

---

## Limitações

- Gera sombras só escurecendo em direção ao preto. Não há versão de realces (clarear).
- A mistura é feita em RGB. Para cores muito saturadas, as sombras mais escuras tendem ao acinzentado.
- Precisa de internet apenas para carregar fontes e iro.js. Sem elas, o app continua funcionando com visual simplificado.

---

## Licença

Uso livre. Adapte, copie e publique como quiser.