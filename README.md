# Greatpages Counter Up

<a href="https://www.buymeacoffee.com/claitonllemes" target="_blank" rel="noopener noreferrer"><img src="https://user-images.githubusercontent.com/99222756/210368404-216273fb-c930-453e-b32b-e3614872eba3.png" width="100%"/></a><br>

## **Configurações**
O código abaixo adiciona animação de contatgem a elementos de texto númericos a uma página na plataforma Greatpages. Copie e cole no menu de configurações da página.

<br><a href="https://www.buymeacoffee.com/claitonllemes" target="_blank" rel="noopener noreferrer"><img src="https://user-images.githubusercontent.com/99222756/210372197-a1d41894-8acc-470b-ac38-2bd1ee0a4ed9.png" width="100%"/></a><br>

```html
<script>

// Name: Counter Up. 
// Version: 1.0.0 
// Copyright© : Claiton Lemes | Alison Zigulich 

    var contadores = $('#e_000000, #e_000000');

    function Contador() {
        if (contadores.length) {
            var janela_top = window.scrollY;
            var janela_bottom = janela_top + $(window).height();
            for (var i = 0; i < contadores.length; i++) {
                var elemento = $(contadores[i]);
                var elemento_top = elemento.offset().top;
                var elemento_bottom = elemento_top + elemento.height();
                if (elemento_bottom > janela_top && elemento_top < janela_bottom) {
                    (function (index) {
                        var elemento_contador = $(contadores[index]);
                        contadores.splice(index, 1);
                        elemento_contador.html(elemento_contador.html().replace('.', ''));
                        var numero = parseInt(elemento_contador.text().match(/[0-9]+/g));
                        elemento_contador.find("span").html(elemento_contador.find("span").html().replace(/[0-9]+/,
                            0));
                        var contador = 0;
                        var contador_somar = parseInt((numero > 200 ? (numero / 200) : 1));
                        var contador_tempo = (numero > 200 ? 10 : (2000 / numero));
                        var contar = setInterval(function () {
                            contador = (contador + contador_somar > numero ? numero : contador +
                                contador_somar);
                            elemento_contador.find("span").html(elemento_contador.find("span").html()
                                .replace(/[0-9]+/, contador));
                            if (contador >= numero) {
                                clearInterval(contar);
                            }
                        }, contador_tempo);
                    })(i);
                    Contador();
                    break;
                }
            }
        }
    }
    $(document).ready(function () {
        setTimeout(function () {
            Contador();
        }, 100);
    });
    $(document).on('resize scroll', function () {
        Contador();
    });
</script>
```