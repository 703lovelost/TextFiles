# Лабораторная №7 - Работа с файловым хранилищем

В лабораторной реализована возможность сохранения текста в txt-файл с возможностью последующего чтения.
При первой загрузке запрашивается разрешение на пользование файловым хранилищем

Метод запроса на пользование хранилищем:

```java
public void onRequestPermissionsResult(int requestCode,
                                           @NonNull String[] permissions,
                                           @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);

        if (requestCode == 1) { // requestCode for saving a text file.

            if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                Toast.makeText(MainActivity.this, "Saving permission granted.", Toast.LENGTH_SHORT).show();
                saveFile();
            }
            else {
                Toast.makeText(MainActivity.this, "Saving permission denied", Toast.LENGTH_SHORT).show();
            }
        } else if (requestCode == 2) { // requestCode for uploading a text file.
            if (grantResults.length > 0
                    && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                Toast.makeText(MainActivity.this, "Uploading permission granted.", Toast.LENGTH_SHORT).show();
                uploadFile();
            }
            else {
                Toast.makeText(MainActivity.this, "Uploading permission denied.", Toast.LENGTH_SHORT).show();
            }
        }
    }
```

Метод сохранения файла:

```java
    private void saveFile() {
        TextView inputEdit = (TextView) findViewById(R.id.editTextTextInput);

        try {
            String text = inputEdit.getText().toString();
            file.createNewFile();
            FileOutputStream fos = new FileOutputStream(file);
            fos.write(text.getBytes());
            fos.close();
            Toast.makeText(this, "Successfully saved!", Toast.LENGTH_SHORT).show();
        }
        catch (FileNotFoundException e)
        {
            e.printStackTrace();
            Toast.makeText(this, "File is not found!", Toast.LENGTH_SHORT).show();
        }
        catch (IOException e)
        {
            e.printStackTrace();
            Toast.makeText(this, "Failed to save a file!", Toast.LENGTH_SHORT).show();
        }
    }
```

Метод загрузки файла:


```java
    private void uploadFile() {
        TextView outputView = (TextView) findViewById(R.id.textViewOutput);

        try {
            FileInputStream fin = new FileInputStream(file);
            byte[] bytes = new byte[fin.available()];
            fin.read(bytes);
            String text = new String(bytes);
            outputView.setText(text);
            fin.close();

        }
        catch (IOException ex) {
            Toast.makeText(this, ex.getMessage(), Toast.LENGTH_SHORT).show();
        }
    }
```
    

Скриншоты приложения и apk-файл включены.
