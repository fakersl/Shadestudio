# shade·studio

Uma cor. Oito tons de sombra.

Um gerador de escalas de cores que funciona direto no navegador. Você escolhe uma cor, ajusta a intensidade e recebe oito tons mais escuros, prontos para usar no seu projeto.

Tudo em um único arquivo HTML, sem instalação, npm ou processo de build.

![Arquivo único](https://img.shields.io/badge/arquivo-único-8d6c98?style=flat-square)
![Sem build](https://img.shields.io/badge/build-nenhum-8d6c98?style=flat-square)
![Tema](https://img.shields.io/badge/tema-claro%20%2F%20escuro-8d6c98?style=flat-square)

---

## Sobre o projeto

A ideia surgiu ao trabalhar com a cor `#E8C5E6`. Eu precisava de tons mais escuros para usar em bordas, textos, botões e outros elementos, mas queria manter as cores consistentes.

Em vez de ajustar cada tom manualmente, o Shade Studio gera uma escala a partir da cor escolhida. Assim, fica mais fácil manter o mesmo padrão em diferentes partes de uma interface ou em projetos diferentes.

## Recursos

- **8 tons de sombra:** do mais claro ao mais escuro.
- **Entrada de cores:** HEX, RGB, HSL, HSV, CMYK e nomes de cores CSS.
- **Seletor visual:** escolha a cor usando o seletor integrado do iro.js.
- **Intensidade ajustável:** controle a diferença entre os tons.
- **Tema claro e escuro:** alterne entre os dois modos e salve sua preferência.
- **Verificação de contraste:** consulte a razão de contraste e os níveis WCAG AA e AAA.
- **Exportação:** copie a escala em CSS variables, JSON ou uma lista de códigos HEX.
- **Prévia:** veja como as cores ficam aplicadas em uma interface de exemplo.
- **Atalhos de teclado:** gere cores aleatórias, troque o tema e copie tons sem precisar clicar em cada botão.

## Como usar

1. Baixe o arquivo `shade-studio.html`.
2. Abra-o no Chrome, Edge, Firefox ou outro navegador compatível.
3. Digite uma cor ou escolha uma pelo seletor.
4. Ajuste a intensidade e copie os tons que quiser usar.

Não é necessário instalar nada. O iro.js e as fontes do Google Fonts são carregados por CDN; se estiver sem internet, o aplicativo usa alternativas locais e o seletor nativo do navegador.

## Como a escala funciona

O Shade Studio escurece a cor original misturando seus valores RGB com preto. Cada nível usa uma proporção diferente, definida pela lista `FACTORS`.

```js
const FACTORS = [.06, .13, .21, .30, .40, .51, .63, .76];
const k = intensidade / 38;

sombra[i] = cor_base * (1 - Math.min(.94, FACTORS[i] * k));
```

Com `#E8C5E6` e a intensidade padrão, a escala fica assim:

| Nível | Nome | HEX |
|---|---|---|
| Base | Original | `#E8C5E6` |
| 01 | Sutil | `#DAB9D8` |
| 02 | Leve | `#CAABC8` |
| 03 | Suave | `#B79CB6` |
| 04 | Média | `#A28AA1` |
| 05 | Firme | `#8B768A` |
| 06 | Densa | `#726171` |
| 07 | Profunda | `#564955` |
| 08 | Abissal | `#382F37` |

Os fatores determinam a intensidade de cada sombra. Você pode alterá-los no código para criar escalas mais suaves ou mais contrastantes.

## Onde usar

**Interfaces:** cores para bordas, estados de hover, botões pressionados, divisores e textos secundários.

**Temas escuros:** tons profundos para fundos e superfícies que mantenham a identidade da cor original.

**Ilustrações e pixel art:** uma sequência de tons para separar luz, meio-tom e sombra.

**Ícones e logos:** variações de uma mesma cor para criar profundidade sem perder a identidade visual.

**Estudos de cor:** uma forma prática de comparar valores e entender como a luminosidade muda em diferentes formatos de cor.

## Exportação

A escala pode ser copiada em três formatos.

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

Também é possível copiar todos os códigos HEX, um por linha.

## Atalhos

| Tecla | Ação |
|---|---|
| `R` | Gerar uma cor aleatória |
| `T` | Alternar o tema |
| `1` a `8` | Copiar um tom |
| `Esc` | Fechar o seletor |
| `Enter` | Confirmar a cor |

## Acessibilidade

- O texto de cada tom recebe uma cor clara ou escura conforme a luminância.
- A razão de contraste pode ser consultada para verificar os critérios WCAG AA e AAA.
- As animações respeitam a preferência `prefers-reduced-motion`.
- Os controles possuem rótulos acessíveis e indicação visual de foco.

## Tecnologias

- HTML, CSS e JavaScript, sem frameworks.
- [iro.js](https://iro.js.org) 5.5.2 para o seletor de cores.
- Google Fonts: Manrope, DM Sans e DM Mono.
- `localStorage` para salvar a preferência de tema.

A transição entre temas usa a View Transitions API quando disponível, com uma alternativa para navegadores que não oferecem suporte.

## Personalização

O código pode ser alterado diretamente no arquivo HTML.

- `FACTORS`: define a progressão das sombras.
- `NAMES`: define os nomes dos níveis.
- `DEF`: define a cor inicial.
- Variáveis CSS em `:root` e `[data-theme="dark"]`: controlam a aparência dos temas.

## Limitações

A escala trabalha apenas com tons mais escuros, sem gerar realces. Como a mistura é feita em RGB, cores muito saturadas podem perder saturação e ficar acinzentadas nos níveis mais profundos.

O seletor visual e as fontes externas dependem de conexão com a internet, mas o restante do aplicativo continua funcionando com as alternativas disponíveis no navegador.

## Licença

Uso livre. Você pode modificar, adaptar e publicar o projeto como quiser.
