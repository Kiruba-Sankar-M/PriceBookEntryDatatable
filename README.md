# PriceBookEntryDatatable
In the Lightning Web Component (LWC), you can select a price book and retrieve the corresponding price book entries to choose the desired products. After selecting products from the entries, you have the option to remove them from the selected products datatable if you no longer wish to include them. Additionally, you can edit the quantity and update it in the database.

![Pricebookentry search functionality](https://github.com/Kiruba-Sankar-M/PriceBookEntryDatatable/assets/121546821/31254770-9a13-41f3-b140-57693d04a423)

![Selected products](https://github.com/Kiruba-Sankar-M/PriceBookEntryDatatable/assets/121546821/78a5040a-1bb2-4c6b-9c6c-579d99b660b3)

You can add this component to the flows and use it to create opportunity line items. If necessary, you can also incorporate this component for billing products, especially if your project involves a billing process.

When you click 'Next', the selected products are passed to the flow as a JSON String. In the flows, you can then convert them back into the required object list.4

<targetConfig targets="lightning__FlowScreen">
    <property name="selectedProducts" type="String" label="Selected Products" description="The selected products." role="outputOnly"/>
</targetConfig>

JOSN DESERIALIZER:

public class JSONDeserialization
{
    @InvocableMethod(label='Get Pricebook Entries from JSON' description='Returns a list of PricebookEntry objects from a JSON string')
    
    public static List<List<PricebookEntry>> getPricebookEntries(List<String> jsonStrings) {
        
        List<List<PricebookEntry>> pricebookEntriesList = new List<List<PricebookEntry>>();
        
        for(String jsonString : jsonStrings) {
            List<PricebookEntry> pricebookEntries = (List<PricebookEntry>) JSON.deserialize(jsonString, List<PricebookEntry>.class);
            pricebookEntriesList.add(pricebookEntries);
        }
        
        system.debug(pricebookEntriesList);
        return pricebookEntriesList;
    }
    
}

Create a text variable in the flow and store the returned JSON string (Selected Products) from the LWC component when you place this component.

![datatable](https://github.com/Kiruba-Sankar-M/PriceBookEntryDatatable/assets/121546821/33c8b87a-474e-4d22-95fa-0b15ac0b14d4)

Now you can loop throught this collection and create opportunity line item or billing line item (If you are working with billing).

That's All!! With ease you can create opportunity line item or billing line item.
