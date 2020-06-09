<script>
  import Select from 'svelte-select';
  import { itemsList } from '../stores/MapInfo.js'
  import { selectedVar } from '../stores/MapInfo.js'

  // the values need to show on interactive component
  let supportRate18, supportRate20, supportRateRecall

  // select box setting
  let inputStyles = 'border-color: #4A75B6; border-style: solid; border-width: 0 0 2px 0;'
  let varList = $itemsList


  let selectedValue = 'OOO';

  // the parameters need to send to stores
  const handleSelectedTown = (e) => {
    selectedVar.update(d => {
            return e.detail.value;
        });
  }

  
</script>


<div class="interactive-panel">
  <div class="slope-highlighter">
    <p>請選擇變數：</p>
    <div class="select-theme">
      <Select items={varList} 
              isSearchable={false}
              {inputStyles}
              isClearable={false}
              {selectedValue}
              on:select="{(e) => handleSelectedTown(e)}">
              </Select>
    </div>
  </div>

  
</div>

<style>
p{
  display: inline-block;
  font-size: 1 em;
  font-family: 'Noto Sans TC';
}
.select-theme{
  font-family: 'Noto Sans TC';
  margin: 0;
  --itemPadding: 0;
  --inputFontSize: 1 em;
  --height: 1 em;
  --inputPadding: 0;
  --borderRadius: 0;
  --selectedItemPadding: 0;
  --indicatorWidth: 0px;
  --border: 0;
  display: inline-block;
}

.select-theme :global(.selectContainer),
.select-theme :global(.selectContainer input){
  --padding: 1px 1px;
}
</style>