<script>
    import { count } from './stores.js';
    export let app_function;
    let numbers = $count;
    let selectedNumberIndex = null;
    let uniqueKeys = Array.from({ length: 10 }, (_, i) => `key-${i + 1}`);
  
    $: {
      numbers = $count;
      uniqueKeys = Array.from({ length: numbers.length }, (_, i) => `key-${i + 1}`);
    }
  
    function addNumber() {
      count.update(n => [...n, n.length + 1]);
    }
  
    function removeNumber() {
      if (numbers.length > 0) {
        count.update(n => n.slice(0, -1));
        if (numbers.length === 1) {
          app_function('Элементов больше нет');
        }
      }
    }
  
    function selectNumber() {
      if (selectedNumberIndex === null) {
        selectedNumberIndex = 0;
      } else {
        selectedNumberIndex = (selectedNumberIndex + 1) % numbers.length;
      }
    }
  </script>

<div class="wrapper">

  <div style="display: flex; justify-content: space-around; margin-top: 20px;">
    <button on:click={addNumber}>Добавить</button>
    <button on:click={removeNumber} disabled={numbers.length === 0}>Удалить</button>
    <button on:click={selectNumber}>Выделить</button>
  </div>
  
  <div style="display: flex; justify-content: space-around;">
    <table>
      <thead>
      <tr>
        <th style="text-align: center">Элементы массива</th>
        <th style="text-align: center">Индексы элементов</th>
        <th style="text-align: center">Уникальные ключи</th>
      </tr>
      </thead>
      {#each numbers as number, index}
      <tbody>
        <tr style:background-color={index === selectedNumberIndex ? 'green' : 'none'}>
          <td style="text-align: center">{number}</td>
          <td style="text-align: center">{index}</td>
          <td style="text-align: center">{Math.floor(Math.random() * 1000)}</td>
        </tr>
      </tbody>
      {/each}
    </table>
  </div>

</div>

<style>
  .wrapper{
      border:1px solid silver;
      border-radius: 30px;
      padding:30px;
  }
</style>