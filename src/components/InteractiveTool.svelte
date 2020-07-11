<script>
  import Select from 'svelte-select';
  import { itemsList, selectedVar } from '../stores/MapInfo.js'

  // select box setting
  let inputStyles = 'border-color: #25877F; border-style: solid; border-width: 0 0 2px 0;'


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
    <p>變數選擇：</p>
    <div class="select-theme">
      <Select items={$itemsList} 
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
.interactive-panel{
  top: 60%;
  right: 10%;
  position: fixed;
  z-index: 2;
}
p{
  display: inline-block;
  font-size: 1.2 em;
  font-family: 'Noto Sans TC';
}
.select-theme{
  font-family: 'Noto Sans TC';
  margin: 0;
  --itemPadding: 0;
  --inputFontSize: 1.2 em;
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
  background: none;
}
</style>