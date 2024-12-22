```bash
npm install react-sortablejs
# or
yarn add react-sortablejs
```

Now, let's create a functional component for the draggable table in React:

```jsx
import React, { useState } from 'react';
import Sortable from 'react-sortablejs';

const DraggableTable = () => {
  const [columns, setColumns] = useState(['Column 1', 'Column 2', 'Column 3']);
  const [data, setData] = useState([
    ['Data 1', 'Data 2', 'Data 3'],
    // Add more rows as needed
  ]);

  const handleSort = (newOrder) => {
    setColumns(newOrder);
    setData((prevData) =>
      prevData.map((row) => {
        const newRow = [...row];
        newOrder.forEach((columnIndex, index) => {
          newRow[index] = row[columnIndex];
        });
        return newRow;
      })
    );
  };

  return (
    <table>
      <thead>
        <tr>
          <Sortable
            items={columns}
            onSort={handleSort}
            options={{ handle: '.handle' }}
          >
            {columns.map((column, index) => (
              <th key={index}>
                {column}
                <span className="handle">⋮</span>
              </th>
            ))}
          </Sortable>
        </tr>
      </thead>
      <tbody>
        {data.map((row, rowIndex) => (
          <tr key={rowIndex}>
            {row.map((cell, cellIndex) => (
              <td key={cellIndex}>{cell}</td>
            ))}
          </tr>
        ))}
      </tbody>
    </table>
  );
};

e
