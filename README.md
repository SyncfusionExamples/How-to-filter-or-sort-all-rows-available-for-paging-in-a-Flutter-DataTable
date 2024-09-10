# How to filter or sort all rows available for paging in a Flutter DataTable (SfDataGrid)?

In this article, we will show how to filter or sort all rows available for paging in a [Flutter DataTable](https://www.syncfusion.com/flutter-widgets/flutter-datagrid).

Initialize the [SfDataGrid](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid-class.html) widget with the necessary properties. To filter or sort all rows available for paging, avoid overriding the [handlePageChange](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridSource/handlePageChange.html) method in the DataGridSource class. The DataGrid will automatically split the rows for each page based on the [SfDataPager.pageCount](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataPager/pageCount.html), which is determined by dividing the total number of DataGridRows by the SfDataPager.pageCount. If you want to control the number of rows per page, you can use the [SfDataGrid.rowsPerPage](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid/rowsPerPage.html) property.

```dart
  late EmployeeDataSource employeeDataSource;
  final int _rowsPerPage = 10;
  final double _dataPagerHeight = 60.0;
  List<Employee> employees = <Employee>[];

  @override
  void initState() {
    super.initState();
    employees = getEmployeeData();
    employeeDataSource = EmployeeDataSource(employeeData: employees);
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Syncfusion Flutter DataGrid'),
      ),
      body: LayoutBuilder(builder: (context, constraint) {
        return Column(children: [
          SizedBox(
              height: constraint.maxHeight - _dataPagerHeight,
              width: constraint.maxWidth,
              child: _buildDataGrid(constraint)),
          SizedBox(
            height: _dataPagerHeight,
            child: SfDataPager(
              delegate: employeeDataSource,
              pageCount: (employees.length / _rowsPerPage).ceil().toDouble(),
            ),
          )
        ]);
      }),
    );
  }

  Widget _buildDataGrid(BoxConstraints constraint) {
    return SfDataGrid(
      source: employeeDataSource,
      rowsPerPage: _rowsPerPage,
      allowFiltering: true,
      allowSorting: true,
      columnWidthMode: ColumnWidthMode.fill,
      columns: <GridColumn>[
        GridColumn(
            columnName: 'id',
            label: Container(
                padding: const EdgeInsets.all(16.0),
                alignment: Alignment.center,
                child: const Text(
                  'ID',
                ))),
        GridColumn(
            columnName: 'name',
            label: Container(
                padding: const EdgeInsets.all(8.0),
                alignment: Alignment.center,
                child: const Text('Name'))),
        GridColumn(
            columnName: 'designation',
            label: Container(
                padding: const EdgeInsets.all(8.0),
                alignment: Alignment.center,
                child: const Text(
                  'Designation',
                  overflow: TextOverflow.ellipsis,
                ))),
        GridColumn(
            columnName: 'salary',
            label: Container(
                padding: const EdgeInsets.all(8.0),
                alignment: Alignment.center,
                child: const Text('Salary'))),
      ],
    );
  }
```

You can download the example from [GitHub](https://github.com/SyncfusionExamples/How-to-filter-or-sort-all-rows-available-for-paging-in-a-Flutter-DataTable).