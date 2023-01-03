# Greatpages Counter Up
 Adiciona animação de contatgem a elementos de texto númericos  na plataforma Greatpages


<br>

<img src="https://user-images.githubusercontent.com/99222756/207317647-1c517d05-a17f-4f25-bbf5-33cbb236e85e.jpg" width="100%"/>

<br>

```html
<script>
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