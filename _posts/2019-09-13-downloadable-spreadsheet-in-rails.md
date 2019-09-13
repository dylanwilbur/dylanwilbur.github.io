---
layout: post
title: How To Make a Rails Model Into A Downloadable Spreadsheet
category: rails-notes
---
This might be useful to do if the data needs to be transported for any reason. The file can be accessed from anywhere after doing this with a `courses_path` request.

## Steps

1.  **Add download links**

    In `index.html.erb` (or wherever you want the buttons to go)
    ```ruby
    <h4>Download:</h4>
    <%= link_to "CSV", courses_path(format: "csv"), class: "btn btn-primary"%>
    <%= link_to "Excel", courses_path(format: "xls"), class: "btn btn-primary"%>
    ```

2.  **Change the index controller action to accommodate serving different file types**

    In `model_controller.rb` 
    ```ruby
    respond_to do |format|
      format.html
      format.csv { send_data @models.to_csv }
      format.xls 
    end
    ```
    
3.   *Add a `to_csv` method to the model's class*

    In `model.rb`
    ```ruby
    def self.to_csv(options = {})
      CSV.generate(options) do |csv|
        csv << column_names
        all.each do |model|
          csv << model.attributes.values
        end
      end
    end
    ```

4.   *Add xls to mime types*
    
    In `config/initializers/mime_types.rb`
    ```ruby
    Mime::Type.register "application/xls", :xls
    ```
    
5.   *Require csv in the model class*
    
    In `model.rb`
    ```ruby
    require 'csv'
    ```
    
6.   *Add an xls format file to serve*
    
    In `index.xls.erb`
    (fill in erb code specific to model)
    ```xml
    <?xml version="1.0"?>
    <Workbook xmlns="urn:schemas-microsoft-com:office:spreadsheet"
      xmlns:o="urn:schemas-microsoft-com:office:office"
      xmlns:x="urn:schemas-microsoft-com:office:excel"
      xmlns:ss="urn:schemas-microsoft-com:office:spreadsheet"
      xmlns:html="http://www.w3.org/TR/REC-html40">
      <Worksheet ss:Name="Sheet1">
        <Table>
          <Row>
            <Cell><Data ss:Type="String">ID</Data></Cell>
            <Cell><Data ss:Type="String">Course Title</Data></Cell>
            <Cell><Data ss:Type="String">Fee(in $)</Data></Cell>
            <Cell><Data ss:Type="String">Created at</Data></Cell>
          </Row>
        <% @courses.each do |course| %>
          <Row>
            <Cell><Data ss:Type="Number"><%= course.id %></Data></Cell>
            <Cell><Data ss:Type="String"><%= product.name %></Data></Cell>
            <Cell><Data ss:Type="Number"><%= product.fee %></Data></Cell>
            <Cell><Data ss:Type="String"><%= product.created_at.to_s("%B %d, %Y")  %></Data></Cell>
          </Row>
        <% end %>
        </Table>
      </Worksheet>
    </Workbook>
    ```
