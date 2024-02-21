
# Popular Companiy Logo

Query to create a table containing the names, site urls and black and white svg logos of companies/applications. 

This table was created using mysql with phpmyadmin, but it contains a table create script as an sql file.

Currently, 75 logos have been shared as svg with only the black and white option included. Original color logos and more company/application logos will be added over time.





## Frequently asked Questions

#### Why?

I needed something like this in my own application and created this table.

#### When will other logos be added?

Other logos will be added over time, but I cannot promise a time. I am open to support.


## Usage/Examples

```php
<!-- Dont forget import select2 library https://select2.org/ -->

<link href="https://cdn.jsdelivr.net/npm/select2@4.1.0-rc.0/dist/css/select2.min.css" rel="stylesheet" />
<script src="https://cdn.jsdelivr.net/npm/select2@4.1.0-rc.0/dist/js/select2.min.js"></script>

<select class="form-select mySelect" id="mySelect" name="mySelect" data-control="select2" data-kt-select2="true">
<?php
    $popular_companies = $your_db_codes("SELECT * from popular_companies");
    foreach ($popular_companies as $company) {
        $name = $company["name"];
        $svg = $company["svg"];
?>
    <option value="<?= $name ?>" data-icon='<?= $svg ?>'>
    <?= $name ?>
    </option>
<?php } ?>
</select>


<script>
    $(document).ready(function () {
        $('#mySelect').select2({
            templateResult: formatIcon,
            templateSelection: formatIcon,
            escapeMarkup: function (m) { return m; }
        });

        function formatIcon(iconOption) {
            if (!iconOption.id) { return iconOption.text; }
            return $('<span style="height:32px; width:32px;"> ' + $(iconOption.element).data('icon') + '' + iconOption.text + '</span>');
        }
    });
    $(".mySelect").select2({
        templateResult: formatState
    });
</script>
