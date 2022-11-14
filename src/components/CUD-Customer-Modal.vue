<!-- Modal for adding new customers -->
<!-- Modal for adding new customers -->
<b-modal
    ref="create-customer-modal"
    hide-footer
    size="xl"
    title="New Customer"
>
<create-customer-form
    @closeCreateModal="closeCreateModal"
    @reloadDataTable="getCustomerData"
    @showSuccessAlert="showAlertCreate"
></create-customer-form>
</b-modal>

<!-- Modal for updating customers -->
<b-modal
    ref="edit-customer-modal"
    hide-footer
    size="xl"
    title="Edit Customer"
>
<edit-customer-form
    :customerId="customerId"
    @closeEditModal="closeEditModal"
    @reloadDataTable="getCustomerData"
    @showSuccessAlert="showAlertUpdate"
></edit-customer-form>
</b-modal>

<!-- Delete Customer Modal -->
<b-modal
    ref="delete-customer-modal"
    hide-footer
    size="md"
    title="Confirm Deletion"
>
<delete-customer-modal
    :customerId="customerId"
    @closeDeleteModal="closeDeleteModal"
    @reloadDataTable="getCustomerData"
    @showDeleteAlert="showDeleteSuccessModal"
></delete-customer-modal>
</b-modal>