# CREATE (POST /events):
  Input → JSON payload
  Auth → Must be host
  Validation → title, datetime, location required
  Result → event inserted, event_id returned

# READ (GET /events):
  Input → filters (club, date, keywords)
  Auth → any user
  Result → list of event objects

# UPDATE (PATCH /events/{event_id}):
  Input → event_id, updated fields
  Auth → event.created_by matches user
  Result → updated row returned

# DELETE (DELETE /events/{event_id}):
  Input → event_id
  Auth → event.created_by matches user
  Result → row removed
