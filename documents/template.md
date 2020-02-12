# Temas para o Template
Temas para apresentação do template [Adianti FrameWork 7.1](https://www.adianti.com.br/)

# Theme3_v4
Para Adianti FrameWork 7.1, *Quais são as diferenças do theme 3 do Adianti ?*. Veja abaixo:

* retirada do `maximum-scale=1, user-scalable=no` da `viewport` no arquivo layout.html. Sem esse parâmetro no celular o usuário consegue fazer o movimento de pinça para aumentar ou diminuir o zoom , o que aumenta acessebilidade para os usuários.
* Inclusão dos arquivos das fontes MaterialIcons e source-code-pro assim não precisa de internet para baixar as fontes. 
* Inclusão do nome do sistema de forma customizada no `application.ini`.
* Inclusão da versão do sistema de forma customizada no `application.ini`.
* Title do HEAD alterado conforme novos parametos `head_title` e `version` no `application.ini`
* Arquivo favicon.png

Locais das alterações
![Theme3_v3](img/theme3_v3.png)


## Origem das fontes MaterialIcons
* MaterialIcons - https://github.com/google/material-design-icons/releases
* source-code-pro - https://github.com/adobe-fonts/source-code-pro
* Artigo do StackOverFlow que ajudou corrigir os temas - https://stackoverflow.com/questions/37270835/how-to-host-material-icons-offline


## Para usar 

### Etapa 01 
Editar o arquivo `<SISTEMA>/app/config/application.ini`

1. Alterar para `theme = theme3_v3`
1. incluindo as informações abaixo : 
```ini
[system]
version = 2.0.0
head_title = Sistema de Exemplo
logo-lg = Exemplo
logo-link-class = SystemAboutView
```
### Etapa 02
Edite o arquivo `<SISTEMA>/app/lib/menu/AdiantiMenuBuilder.php` incluido as linhas abaixo:
```php
            case 'theme3_v3':
                    ob_start();
                    $xml = new SimpleXMLElement(file_get_contents($file));
                    $menu = new TMenu($xml, null, 1, 'treeview-menu', 'treeview', '');
                    $menu->class = 'sidebar-menu';
                    $menu->id    = 'side-menu';
                    $menu->show();
                    $menu_string = ob_get_clean();
                    return $menu_string;
                    break;  
```

### Etapa 03
Edite o arquivo `<SISTEMA>/index.php` incluido as linhas abaixo:

```php
$system_version = $ini['system']['version'];
$head_title  = $ini['system']['head_title'].' - v'.$system_version;
$content     = str_replace('{head_title}', $head_title, $content);
$content     = str_replace('{system_version}', $system_version, $content);
$content     = str_replace('{logo-mini}', $ini['general']['application'], $content);
$content     = str_replace('{logo-lg}', $ini['system']['logo-lg'], $content);
$content     = str_replace('{logo-link-class}', $ini['system']['logo-link-class'], $content);
```