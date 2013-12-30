Model Evaluation
================

Confusion Matrix
----------------


<table class="table confusion-matrix">
    <thead>
        <tr>
            <th>Actual / Predicted</th>
            <th>Positive</th>
            <th>Negative</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th>Positive</th>
            <td>True Positive</td>
            <td>False Negative</td>
        </tr>
        <tr>
            <th>Negative</th>
            <td>False Positive</td>
            <td>True Negative</td>
        </tr>
    </tbody>
</table>

Derivations
-----------

* Precision, HitRate

$$Precision = HitRate = {TP \over ActionRecords} = {TP \over TP+FP}$$

*  True Positive Rate(TPR), Sensitivity, Recall, CatchRate,

$$TPR=Sensitivity=Recall=CatchRate= {TP \over AllPos} = {TP \over TP+FN}$$

* Specificity

$$Specificity= {TN \over AllNeg}= {TN\over TN+FP}$$

* False Positive Rate(FPR)

$$FPR=1-Specificity= {FP \over AllNeg}= {FP\over TN+FP}$$

* ActionRate

$$ ActionRate = {ActionRecords \over AllRecords} = {TP+FP \over AllRecords}$$

* F-measure / F1 Score

$$ F_1 = 2\cdot {Precision \cdot Recall \over Precision + Recall}$$

### Illustration
<div id="confusionmat-illustration">
<div class="row">
    <div class="col-md-4">
        <div class="illustration-button" id="tpr">TPR</div>
        <div class="illustration-button" id="fpr">FPR</div>
        <div class="illustration-button" id="precision">Precision</div>
        <div class="illustration-button" id="recall">Recall</div>
        <div class="illustration-button" id="cr">CatchRate</div>
        <div class="illustration-button" id="hr">HitRate</div>
        <div class="illustration-button" id="ar">ActionRate</div>
    </div>
    <div class="col-md-8" id="formula">
        <div id="dummy-math">$$ N/A $$</div>
        <div id="tpr-math" style="display:none">$$= {TP \over TP+FN}$$</div>

        <div id="fpr-math" style="display:none">$$= {FP\over TN+FP}$$</div>

        <div id="precision-math" style="display:none">$$= {TP \over TP+FP}$$</div>

        <div id="ar-math" style="display:none">$$= {TP+FP \over TP+FP+TN+FN}$$</div>
        
    
        <table class="table confusion-matrix" >
            <thead>
            
                <tr>
                    <th></th>
                    <th>Predicted<br>Pos</th>
                    <th>Predicted<br>Neg</th>
                </tr>
            </thead>
            <tbody>
                <tr>
            
                    <th>Actual<br>Pos</th>
                    <td id="tp">TP</td>
                    <td id="fn">FN</td>
                </tr>
                <tr>
                    <th>Actual<br>Neg</th>
                    <td id="fp">FP</td>
                    <td id="tn">TN</td>
                </tr>
            </tbody>
        </table>
    </div>
</div>
</div>

Curves
------

### Receiver Operating Characteristic (ROC)

* x-Axis: FPR
* y-Axis: TPR

### Precision-Recall (PR)

* x-Axis: Recall
* y-Axis: Precision

### Lift

* model vs random = current TP vs current Total * bad Rate

### Gain

 current TP / # bad



<script>

var activeColor = "steelblue",
    defaultColor = "white",
    border="5px solid black";

function tpr_mouseover() {
    $('#tpr-math, #fpr-math, #precision-math, #ar-math, #dummy-math').hide();
    $('#tpr-math').show();

    $('#tp, #fp, #tn, #fn')
        .css('background-color', defaultColor)
        .css('border', 'none')
    $('#tp')
        .css('background-color', activeColor)
        .css('border', border)
        .css('border-style', 'solid none solid solid')
    $('#fn')
        .css('border', border)
        .css('border-style', 'solid solid solid none')
}

function fpr_mouseover() {
    $('#tpr-math, #fpr-math, #precision-math, #ar-math, #dummy-math').hide();
    $('#fpr-math').show();
    $('#tp, #fp, #tn, #fn')
        .css('background-color', defaultColor)
        .css('border', 'none')

    $('#fp')
        .css('background-color', activeColor)
        .css('border', border)
        .css('border-style', 'solid none solid solid')
    $('#tn')
        .css('border', border)
        .css('border-style', 'solid solid solid none')
}

function precision_mouseover() {
    $('#tpr-math, #fpr-math, #precision-math, #ar-math, #dummy-math').hide();
    $('#precision-math').show();

    $('#tp, #fp, #tn, #fn')
        .css('background-color', defaultColor)
        .css('border', 'none')
    $('#tp')
        .css('background-color', activeColor)
        .css('border', border)
        .css('border-style', 'solid solid none solid')
    $('#fp')
        .css('border', border)
        .css('border-style', 'none solid solid solid')
}

function ar_mouseover() {
    $('#tpr-math, #fpr-math, #precision-math, #ar-math, #dummy-math').hide();
    $('#ar-math').show();

    $('#tp, #fp, #tn, #fn')
        .css('background-color', defaultColor)
        .css('border', 'none')
    $('#tp, #fp')
        .css('background-color', activeColor)
    $('#tp')    
        .css('border', border)
        .css('border-style', 'solid none none solid')
    $('#fp')
        .css('border', border)
        .css('border-style', 'none none solid solid')
    $('#fn')
        .css('border', border)
        .css('border-style', 'solid solid none none')
    $('#tn')
        .css('border', border)
        .css('border-style', 'none solid solid none')
}

$(document).ready(function() {
    $('#tpr, #recall, #cr').mouseover(tpr_mouseover);
    $('#fpr').mouseover(fpr_mouseover); 
    $('#precision, #hr').mouseover(precision_mouseover);
    $('#ar').mouseover(ar_mouseover);    
    
})

</script>